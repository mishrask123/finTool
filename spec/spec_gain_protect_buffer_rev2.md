# Spec — Gain-Protection Buffer & Stop Ratchet

**Owner:** PM (Saman Mishra) · **Drafted:** 2026-09-12 · **Rev 2:** 2026-09-12 · **Status:** DRAFT for review
**Implements:** `recon --protect` (proposed new mode)
**Scope:** long-only rotational equity book, ~250–500 names, $2–2.5k per name (~50bps of equity)

---

## 1. Purpose

Set and maintain a **stop price per position** that protects accumulated gain, calibrated to each
name's own volatility and modulated by where the name sits in its alpha cycle. Emit a daily order
plan. Never place a stop that sits below cost.

**Non-goals.** This does not size positions, does not initiate, and does not decide exits on
loss-making positions. Underwater names are a separate discretionary process (§9 DRIFT panel).
Hedges are out of scope entirely (§3.4).

---

## 2. Inputs

### 2.1 `eod_rsi.tsv` — assumed available, one row per Symbol per Date

| Field | Type | Notes |
|---|---|---|
| `Date` | date | trading date, EOD |
| `Symbol` | str | |
| `Close` | dec | split/div adjusted |
| `Volume` | int | |
| `RSI14` | 0–100 | Wilder, 14 sessions. **Low = washed** |
| `VEL20` | 0–100 | 20-session momentum rank. **High = turning up** |
| `DIST50` | dec | `(Close − MA50)/MA50`, signed. **Negative = below trend** |
| `SIGMA20` | pct | percent per day. **Computed per §3A — that section is normative** |
| `SIGMA60` | pct | percent per day, 60-session window. Regime-shift check, §3A.6 |
| `ATR14` | pct | ATR as % of Close. Fallback only, §3A.5 |
| `MA20`,`MA50`,`MA200` | dec | |
| `DataDays` | int | sessions of history available for this Symbol |

### 2.2 `positions.tsv` — one row per **lot**

`Account · SubAccount · Symbol · LotId · LotDate · Qty · AvgCost · Price · MktValue · BookTag`

### 2.3 `benchmark.tsv`

`Date · BenchSymbol · Close · Ret1D · Ret20D · Ret60D`

### 2.4 `meta.tsv`

`Symbol · Sector · Industry · Bench · Beta · Float · ShortPctFloat · DTC`

### 2.5 `signal.tsv` — from the prealpha/converge run

`Symbol · AsOfDate · Model · PeakT · Score · Prob`

### 2.6 `stop_state.tsv` — **STATE FILE, read and written every run**

`Symbol · Account · SubAccount · HighWaterPrice · BufferPct · StopPrice · Regime · FirstSetDate · LastUpdated`

> **This file does not exist today and is the single hardest requirement.** The ratchet is
> monotonic (§7); without persisted high-water and prior stop, the stop can be lowered by a
> down day, which defeats the whole design. If it is absent on first run, initialise
> `HighWaterPrice = Close` and `StopPrice = 0` for every position.

### 2.7 `k_band.tsv` — **PM-maintained, set once per name**

`Symbol · KBand · KSource · SetDate · SetBy · Note`

`KBand ∈ {8, 10, 12, 15, 20}`. `KSource ∈ {SEED, MANUAL}`.

**This file is not computed and is never recalculated by the engine.** It is the PM's
discretionary input, written once when a name first becomes protectable and changed only by
explicit PM action. See §7.1.

---

## 3. Conventions — pin these or the multiplier inverts

1. **`SIGMA20` is percent per day**, computed exactly as §3A. `SIGMA20 = 1.25` means 1.25%/day.
   Declare the unit in the file header. **Do not** reuse `liquidty.tsv`'s `Volatility` — its unit
   is undocumented and the buffer scales linearly with it.
2. **`RSI14` low = washed / oversold.** 0–100.
3. **`VEL20` high = turning up.** 0–100 rank.
4. **`DIST50` is signed raw**, not a percentile. Negative = below the 50-day. This is the
   opposite sign to `demand_converge.D_DIST`, where high means washed. Convert on load.
5. **`BookTag ∈ {BOOK, HEDGE, LTCG_HOLD}`.** Only `BOOK` is processed. `HEDGE` is excluded —
   a stop on a hedge removes protection exactly when the hedged risk fires.
6. All percentages as decimals internally (0.15), formatted on output.

---

## 3A. SIGMA20 — normative calculation

The buffer scales linearly with this number, so it is specified exactly. Any deviation changes
every stop price in the book.

### 3A.1 Source series

Split- and dividend-**adjusted** closes, one per trading session, ascending by date. If only
unadjusted closes are available, §3A.7 applies.

### 3A.2 Returns

```
r_t = ln( C_t / C_{t-1} )            natural log, simple daily
```

Log rather than arithmetic returns: they are additive across days, symmetric for up and down
moves, and make the √n drawdown scaling in §7.1 exact rather than approximate.

### 3A.3 Window

The **20 most recent completed sessions**, i.e. `r_{t-19} … r_t` where `t` is the EOD date of the
file. That requires **21 closes**. Today's close is included — the file is EOD.

Sessions are trading sessions, not calendar days. A halted or non-traded day is **skipped, not
zero-filled**: a halt is absence of information, not a 0% return, and zero-filling biases σ down.

### 3A.4 Estimator

```
mean  = ( Σ r_i ) / n                             n = 20
var   = ( Σ (r_i − mean)^2 ) / (n − 1)            sample variance, Bessel corrected
SIGMA20 = sqrt(var) × 100                         percent per day
```

Do **not** assume zero mean. Over 20 sessions a trending name has a materially non-zero drift,
and forcing mean = 0 inflates σ by folding the trend into the dispersion — which would widen the
stop precisely on the names that are working.

### 3A.5 Winsorising

Before computing variance, clip each `r_i` to ±5 × `SIGMA60_prev` (yesterday's 60-day sigma).
Purpose: one data error, an unadjusted split, or a single gap event cannot dominate a 20-day
window. If `SIGMA60_prev` is unavailable, clip at ±25% log return.

Fallback order if `SIGMA20` cannot be computed:

1. `ATR14 / Close × 100` — comparable scale, different estimator, acceptable substitute.
2. Sector median `SIGMA20` — **flagged**, not silently substituted.
3. Otherwise `NO_GATE`, reason `NO_VOL`. No order.

### 3A.6 Smoothing and regime check

The raw 20-day estimate jitters day to day. Use:

```
SIGMA_USED = median( SIGMA20_t , SIGMA20_{t-1} , … , SIGMA20_{t-4} )        5-day median
```

A median rather than a mean so a single event day does not move the buffer.

Additionally compute `SIGMA60` on the same estimator over 60 sessions. If
`SIGMA20 / SIGMA60 > 2.0`, set `VolRegimeShift = TRUE` — the 20-day window is capturing an event
(earnings gap, guidance cut, M&A). Report it. Do not auto-widen: a regime shift is a reason for
the PM to look, not for the engine to loosen a stop.

### 3A.7 Corporate actions

With adjusted closes this is handled upstream. With unadjusted closes, if
`|r_t| > 0.35` and `Volume_t < 3 × median(Volume_{t-20..t-1})`, treat it as a suspected
unadjusted corporate action: **halt that symbol**, emit no order, and require the PM to re-seed
`HighWaterPrice` in `stop_state.tsv`. A 35% move on ordinary volume is far more likely a split
than a real print.

### 3A.8 Asymmetry note — why daily σ drift is safe

`SIGMA_USED` updates daily, so `buf` drifts daily. That does not destabilise the stop, because
of the ratchet in §7.6:

- **σ rises → buf widens → `HighWater × (1 − buf)` falls → `max(prior, raw)` keeps the prior
  stop.** A volatility spike cannot loosen an existing stop.
- **σ falls → buf narrows → raw rises → the stop tightens.**

So σ drift is **one-directional in effect: it can only tighten.** Combined with
`amend_threshold`, AMEND churn is bounded and always in the protective direction.


---

## 4. Position aggregation

Group lots to `(Symbol, Account, SubAccount)` — the level at which an order is placed.

```
Qty      = Σ lot.Qty
Cost     = Σ (lot.Qty × lot.AvgCost)
C        = Cost / Qty                      weighted average cost
P        = Close from eod_rsi (today)
G        = P/C − 1                          unrealized gain, decimal
AgeMax   = today − min(lot.LotDate)         oldest lot, calendar days
AgeWtd   = Σ(lot.Qty × age) / Qty           weighted age
LTCG_d   = 365 − AgeMax                     days to long-term treatment, if > 0
```

Keep `AgeMax` for the drift check and `LTCG_d` as an output column — it informs discretion
without driving the formula.

---

## 5. Eligibility gate

Process a position only if **all** hold:

```
BookTag == BOOK
Qty > 0
G >= 0.10                       ◄ the 10% gain gate
DataDays >= 20                  ◄ the 20-session minimum
SIGMA20 is present and > 0
eod_rsi.Date == last trading day (staleness guard, §10)
```

Anything failing the gate emits **no order** and is written to `stop_plan.tsv` with
`Regime = NO_GATE` and a reason code. Positions with `G < 0.10` are not errors — they are simply
not yet protectable, and they graduate automatically as they appreciate.

---

## 6. Regime classification

Computed before the buffer, because at two of the four regimes the **instrument changes**, not
just the number.

```
PeakExpired = signal.PeakT is not null
              AND (today − signal.AsOfDate) >= signal.PeakT

RS20        = Ret20D(Symbol) − Ret20D(meta.Bench)        relative strength, 20 sessions
RSDecay     = RS20 < 0 AND Ret20D(Symbol) < 0            losing to its own benchmark, absolutely
```

| Regime | Condition (first match wins) | Instrument |
|---|---|---|
| **R3 ALPHA_SPENT** | `RSI14 >= 80` OR `PeakExpired` OR (`VEL20 < 20` AND `RSDecay`) | tighten hard, §7.3 |
| **R1 ALPHA_AHEAD** | `RSI14 < 20` AND `VEL20 >= 60` AND `DIST50 < 0` AND NOT `PeakExpired` | **no stop** — §6.1 |
| **R2 ALPHA_WORKING** | otherwise | buffer + ratchet, §7 |

### 6.1 Why R1 emits no order

A washed name turning up with velocity, still inside its predicted peak horizon, is early in its
move. The widest possible buffer is the absence of an order. A stop here is a tax on a thesis that
has not yet played out, and the gain being protected is small by construction. Emit
`Regime = ALPHA_AHEAD, Action = NONE` and carry `HighWaterPrice` forward so the position enters
R2 already ratcheted when RSI normalises.

---

## 7. Buffer and stop

### 7.1 Base scale — banded k, manually set once

```
k    = k_band.tsv[Symbol].KBand            ∈ {8, 10, 12, 15, 20}
base = k × SIGMA_USED                      §3A.6
```

`k` is **the PM's one discretionary input per name**, and it answers a question no formula can:
`k` is noise tolerance, `k × σ` is give-back tolerance, and on a high-σ name the two conflict
directly. Choosing the band is choosing which of the two to honour.

Read `k` as *how many of this name's own typical days the stop tolerates*. At `k = 15` the name
must fall fifteen typical days' worth below its high-water mark before the stop fires.

**Provenance of the band values.** They are not fitted. The PM's stated preference — a 15% buffer
on high-beta names — implies `k ≈ 10–14` on the book's high-σ names (AXTI 9.8, POET 10.5,
NVTS 11.9, QBTS 12.9, BE 13.0, ASTS 13.5, APLD 14.3 as of 2026-09-11). The ladder brackets that
with room either side. Model-based calibration is deferred until signal-path history exists;
realized-lot history is **not** a valid calibration source, since those lots were exited under
discretion rather than under this rule.

#### 7.1.1 Lifecycle — set once

| Event | Behaviour |
|---|---|
| Symbol first becomes gate-eligible and has no `k_band` row | write a row with the §7.1.2 seed, `KSource = SEED`, and **emit no order that day** — the PM reviews the seed first |
| `k_band` row exists | use it. The engine never recomputes or overrides it |
| PM edits the band | `KSource = MANUAL`, new `SetDate`. Takes effect next run |
| Position exited | **keep the row.** A re-entry inherits the prior band and the reasoning behind it |
| σ regime shift (§3A.6) | report `VolRegimeShift`; do **not** change the band |

The band is deliberately sticky. A buffer that re-derives itself daily cannot be audited, because
you can never separate the PM's judgment from the model's drift. A sticky band can: in six months
"which band was this on when it stopped, and was that right?" has an answer.

#### 7.1.2 Seed ladder — first fill only, a suggestion not a rule

```
SIGMA_USED  < 0.40   →  k = 20
            < 0.70   →  k = 15
            < 1.00   →  k = 12
            < 1.30   →  k = 10
            >= 1.30  →  k =  8
```

The ladder **lowers** `k` as σ rises, trading more noise-exits for less give-back on the wild
names. That is a stated preference, not a derivation — invert it if the PM would rather hold
through the chop. Every seeded row requires PM confirmation before its first order (§7.1.1).

### 7.2 Alpha multiplier

```
m = 1.0
RSI14 >= 80              m *= 0.65
RSI14 in [60, 80)        m *= 0.85
RSI14 in [20, 60)        m *= 1.00
RSI14 <  20              m *= 1.20
VEL20 >= 60              m *= 1.10
VEL20 <  20              m *= 0.90
PeakExpired              m *= 0.70
RSDecay                  m *= 0.85
AgeMax > 100 days        m *= 0.90        ◄ drift discount, not a gate
```

Multiplicative and order-independent. Effective range ≈ 0.35 – 1.45.

### 7.3 R3 override

In ALPHA_SPENT, cap the multiplier: `m = min(m, 0.70)`. The purpose of R3 is harvest, so the stop
should be close enough that ordinary weakness completes the exit.

### 7.4 Clamp — the part that does the actual work

```
lo  = max(0.03, 8 × SIGMA20)                never inside 8 sigma-days
hi  = min(0.30, G / (1 + G))                ◄ THE GAIN CONSTRAINT
buf = clamp(base × m, lo, hi)
```

**Proof that `hi = G/(1+G)` guarantees the stop never sits below cost.** With `P = C(1+G)`:

```
stop = P × (1 − G/(1+G))
     = C(1+G) × ( 1/(1+G) )
     = C                            exactly breakeven
```

So any `buf ≤ G/(1+G)` yields `stop ≥ C`. The constraint is structural, not a post-hoc check.
The buffer yields to the gain rather than competing with it.

| G | max buffer | | G | max buffer |
|---|---|---|---|---|
| 10% | 9.09% | | 30% | 23.08% |
| 15% | 13.04% | | 50% | 33.33% |
| 20% | 16.67% | | 100% | 50.00% |

**The clamp overrides the band, and is never manual.** `hi = G/(1+G)` is arithmetic, not
judgment — it is the guarantee that the stop never sits below cost. If it were overridable the
guarantee collapses. When `base × m > hi` the band is advisory and `buf = hi`; report
`BandClamped = TRUE` so the PM can see the band is not binding.

**If `lo > hi`** — the name is too volatile to protect this gain without sitting inside its own
noise — emit `Regime = UNPROTECTABLE, Action = NONE` and flag it. Do **not** place the stop.
*Worked case, 2026-09-11: AXTI at G = 12.66%, σ = 1.53. Even `k = 8` gives 12.3% while the gain
allows only 11.2%. No band setting protects it; the correct output is no order.*
This is the single most important guard in the spec; it is the case that produced 68 names with
stops below cost in the 2026-09-11 book.

### 7.5 Locked floor (output, not input)

```
floor = (1 − buf) × (1 + G) − 1              guaranteed >= 0 by §7.4
```

### 7.6 Ratchet — monotonic

```
HighWaterPrice = max(prior HighWaterPrice, P)
raw            = HighWaterPrice × (1 − buf)
StopPrice      = max(prior StopPrice, raw)          never decreases
```

Anchoring to `HighWaterPrice` rather than today's `P` means a down day cannot loosen the stop.
`StopPrice` is monotonic non-decreasing for the life of the position. It changes only when the
position makes a new high or the buffer tightens.

### 7.7 Order emission

```
Action = NEW      if no live stop order exists
         AMEND    if |StopPrice − live order stop| / live > amend_threshold   (default 0.005)
         HOLD     otherwise
         NONE     R1, NO_GATE, UNPROTECTABLE
```

`amend_threshold` exists to suppress churn. The broker's trailing-stop type is **not** relied on:
every order is a plain stop-limit at an explicit price, re-issued on AMEND. `LimitPrice =
StopPrice × (1 − limit_offset)`, `limit_offset` default 0.01, widened to 0.02 where
`SIGMA20 > 1.0` so the limit is not skipped in a gap.

---

## 8. Cluster guard — run after all positions are computed

Per-name stops are individually sound and collectively dangerous: they are geared to the same
factors and fire together.

```
for each candidate stop:
    shock_move  = −5% × meta.Beta
    would_fire  = shock_move <= −buf

cluster_value = Σ MktValue where would_fire
cluster_pct   = cluster_value / book_equity
```

If `cluster_pct > cluster_cap` (default **0.08**), do not silently place everything. Rank
candidates by `floor` descending and place only down to the cap; the remainder emit
`Action = NONE, Reason = CLUSTER_CAP`. Report the full list either way.

*On the 2026-09-11 book, a naive run would have had 12.7% of the trading book stopping out on a
single −5% index day.* The cap is the control for that.

Additionally, suppress **all** AMEND/NEW emission on `T−1` and `T` of a scheduled FOMC, CPI or
major-index-rebalance date, configurable in `event_blackout.tsv`. Rationale: placing forty stops
the day before a coin-flip macro event maximises correlated noise exits.

---

## 9. DRIFT panel — separate output, no orders

The 100-day rule is **discretionary drift detection, not a gate.** Emit
`drift_panel.tsv` for every `BOOK` position where `G < 0`:

`Symbol · MktValue · G · AgeMax · AgeWtd · Ret20D · Bench · BenchRet20D · RS20 · Sector ·
SectorRet20D · RSI14 · VEL20 · DIST50 · PeakT · PeakExpired · SleeveWeight · LTCG_d`

Sort by `RS20` ascending (worst relative performance first). No recommendation, no order — the
panel exists so discretion has its inputs in one place. Biotech is tagged and excluded from any
ranking: its alpha is event-driven, so RSI and velocity do not describe it, and it is handled by
the separate catalyst-calendar process.

---

## 10. Guards and edge cases

| Case | Behaviour |
|---|---|
| `eod_rsi.Date` older than last trading day | **abort the whole run**, emit nothing, alert. Never place orders off stale data |
| `SIGMA20` null or 0 | fall back to `ATR14`; if also missing → `NO_GATE`, reason `NO_VOL` |
| `DataDays < 20` | `NO_GATE`, reason `SHORT_HISTORY` |
| `lo > hi` | `UNPROTECTABLE` (§7.4) |
| Symbol absent from `eod_rsi` | `NO_GATE`, reason `NO_PRICE`, alert |
| Position exited but stop order live | emit `Action = CANCEL` (orphan sweep) |
| Multiple accounts, same symbol | independent stop per account; buffer identical, `StopPrice` may differ by cost basis |
| Warrants, units, ADR ratio changes | `BookTag = LTCG_HOLD` or exclude; `OXYWS`-type instruments are not stop-manageable |
| Corporate action / split | if `|Close_t / Close_{t−1} − 1| > 0.35` and no matching volume spike, halt that symbol and require manual re-seed of `HighWaterPrice` |
| Earnings within 2 sessions | `m *= 1.15` (widen) — do not get stopped by a scheduled event |

---

## 11. Outputs

### 11.1 `stop_plan.tsv` — daily

`RunDate · Symbol · Account · SubAccount · Qty · C · P · G · AgeMax · Regime · SIGMA20 ·
SIGMA60 · SIGMA_USED · VolRegimeShift · KBand · KSource · base · m · lo · hi · BufferPct ·
BandClamped · HighWaterPrice · StopPrice · LimitPrice · FloorLocked · Action · Reason ·
ClusterFlag · Bench · RS20 · Sector`

### 11.2 `stop_state.tsv` — rewritten each run (§2.6)

### 11.3 `drift_panel.tsv` — §9

### 11.4 `run_summary.txt`

Counts by regime and action; `cluster_pct`; names entering/leaving the gate; every `UNPROTECTABLE`
and `CANCEL`; any halted symbol.

---

## 12. Acceptance tests

1. **Floor never negative.** For every row with `Action ∈ {NEW, AMEND}`: `FloorLocked >= 0` and
   `StopPrice >= C`. Zero exceptions permitted.
2. **Monotonic ratchet.** Replay 60 sessions: `StopPrice` never decreases for a continuously held
   position.
3. **Gain constraint binds.** Construct `G = 0.12, SIGMA20 = 1.5` → `base = 0.225`,
   `hi = 0.107` → `buf = 0.107`, `floor ≈ 0`. Assert the clamp fires.
4. **Unprotectable detected.** `G = 0.10, SIGMA20 = 1.5` → `lo = 0.12 > hi = 0.0909` →
   `UNPROTECTABLE`, no order.
5. **Gate.** `G = 0.099` → `NO_GATE`. `G = 0.100` → processed.
6. **Regime precedence.** `RSI14 = 85` AND `VEL20 = 70` AND `DIST50 < 0` → `ALPHA_SPENT`,
   not `ALPHA_AHEAD`.
7. **Hedge exclusion.** `BookTag = HEDGE` → never appears in `stop_plan` with an action.
8. **Cluster cap.** Synthesise 40 beta-3 positions at `buf = 0.12` → `cluster_pct > 0.08` →
   partial placement, remainder `CLUSTER_CAP`.
9. **Staleness abort.** `eod_rsi.Date = T−2` → run aborts, zero orders.
10. **Band stickiness.** Run 20 sessions with σ drifting across a ladder boundary. Assert
    `KBand` never changes without a `SetDate` edit, and `KSource` is preserved.
11. **Seed requires confirmation.** A newly gate-eligible symbol with no `k_band` row emits
    `Action = NONE` on its first run, and a row with `KSource = SEED`.
12. **Band survives exit.** Exit and re-enter a symbol; assert the `k_band` row and `SetDate`
    are unchanged.
13. **Clamp beats band.** `KBand = 20`, `σ = 1.5`, `G = 0.15` → `base = 0.30`, `hi = 0.130` →
    `buf = 0.130`, `BandClamped = TRUE`.
14. **σ asymmetry.** Double `SIGMA_USED` on one session; assert `StopPrice` does not fall
    (§3A.8). Halve it; assert `StopPrice` rises or holds.
15. **σ estimator.** Feed a known 21-close series; assert `SIGMA20` matches an independent
    Bessel-corrected log-return stdev to 1e-9. Assert a zero-mean assumption is *not* used.
16. **Winsorising.** Inject a single +40% return into an otherwise 1%/day series; assert
    `SIGMA20` moves less than 15%.
17. **Forward paper-run, not backtest.** Log `stop_plan` daily for 4–6 weeks with all `Action`
    suppressed. Compare would-have-fired events against PM judgment before any live order.
    Realized-lot history is explicitly **not** a calibration source (§7.1).

---

## 13. Defaults

```
k                 PER NAME  from k_band.tsv, one of {8,10,12,15,20}, manual, set once
sigma_window      20        sessions, log returns, Bessel-corrected (§3A)
sigma_smooth      5         day median of SIGMA20
sigma_winsor      5         x SIGMA60_prev
regime_shift      2.0       SIGMA20/SIGMA60 ratio that flags VolRegimeShift
lo_abs            0.03      absolute minimum buffer
lo_sigma          8         minimum in sigma-days
hi_abs            0.30      absolute maximum buffer
gain_gate         0.10      minimum G to protect
min_history       20        sessions
amend_threshold   0.005     suppress order churn
limit_offset      0.01      0.02 if SIGMA20 > 1.0
cluster_cap       0.08      of book equity
earnings_widen    1.15
drift_age         100       days, discount only
```

---

## 14. What I need that does not exist today

Ordered by how much each blocks the build.

1. **`k_band.tsv`** — PM-maintained band per name (§2.7). One integer each, set once. Nothing
   can be placed without it.
2. **`stop_state.tsv`** — the ratchet memory. Without persisted `HighWaterPrice` and
   `StopPrice`, §7.6 is impossible and the stop can fall on a down day. Nothing else matters
   until this exists.
3. **Lot-level dates in the position export.** The 2026-09-11 Merrill export carries no
   `LotDate`; ages had to be recovered from the 09-04 `pnl` snapshot. `AgeMax`, `AgeWtd`,
   `LTCG_d` and the drift discount all depend on it.
4. **`BookTag` per position.** OXY/OXYWS are hedges, not trades. Without the tag every
   aggregate is wrong and the engine would try to stop the hedge. PBR's status is also
   undetermined.
5. **`SIGMA20` and `SIGMA60` computed per §3A**, with the unit declared in the file header.
   `liquidty.tsv`'s `Volatility` is not a substitute — undocumented unit, unknown window,
   unknown estimator.
6. **`Bench` per symbol and benchmark return series.** `demand_converge` carries `Bench`
   (SMH/SOXX/XLK/XBI/IHI/PICK); the return series to compare against is not in the tablet set.
7. **Sector/industry return series** for the drift panel's sector column.
8. **`event_blackout.tsv`** — FOMC, CPI, index rebalance dates.
9. **Sleeve definition table** — `Symbol → Sleeve`, so §8 and the drift panel can report
   sleeve weight. Semis/AI, biotech, energy, rates-sensitive at minimum.

### Known-bad inputs to fix upstream first

- `RealizedPnlPct` in `pnl_realized_lots.tsv` is unusable — SMH shows +1.5% on $13,200 of
  profit. Recompute from `RealizedPnl / AcquisitionCost`.
- `dd`, `smooth` are constant across all 111 rows of `mm_prealpha/invest.tsv`; `ear` is
  108/111. Zero information.
- The liquidity leg (`liquidity`, `liq`, `cross_otc_x_liq`, `cross_trend_x_liq`) is 0 on
  111/111.
- 14 of 66 screened names have no row in `otc_aggregate.tsv` at all, so `otc = 0` means
  *unmeasured*, not neutral.
- `mm_prealpha/invest.tsv` carries `asofdate 2026-08-31` while living in a folder named
  `20260902`. Folder name ≠ data date. `PeakExpired` must use `AsOfDate`, never the path.

---

## 15. Open decisions for the PM

1. Seed ladder direction (§7.1.2) — `k` falls as σ rises. Confirm, or invert to hold through
   chop on the high-σ names?
2. `gain_gate = 10%` — **confirmed by PM.**
3. Banded manual `k`, set once — **confirmed by PM.** Realized-history calibration dropped.
4. `cluster_cap = 8%` of equity — right tolerance?
5. Does R1 ALPHA_AHEAD emit **no** stop, or a wide disaster floor?
6. Should `LTCG_d < 30` widen the buffer to defer a short-term realization, or stay
   discretionary?
7. Is PBR hedge or book?
8. Cadence: daily EOD, or weekly with a daily exception scan?
9. Rollout: start with the nine σ < 0.40 names, where the gain constraint never binds and no
   band judgment is needed, then extend to the high-σ tier?
