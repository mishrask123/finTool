# Buffer & k-bands — primer for a Claude agent

**Written 2026-09-14.** Self-contained: paste this whole file into a fresh session. It explains
the gain-protection buffer mechanism, the k-band system, and **one confirmed unit error in the
spec that must be fixed before anyone implements it.**

Canonical spec: `quantbot/tablet/spec_gain_protect_buffer_rev2.md`
(id `1N5o-GQ9qVuB3ebRGcu9dgB7mXEKqpnTO`). This primer **supersedes the spec's numeric values**
per §6 below. The spec's *structure* is sound; its *constants* are not.

---

## 1. What the mechanism is for — in the PM's own words

> *"I want to protect gain using stop loss based on my desired positive pnl% ++, this I call on
> strength. The pnl% generally on beta how stock moves, discretionary and has age i.e. how long I
> hold position. If a stock moves positively, i.e. alpha is still there I will adjust stop limit
> price as long as alpha is there. This must be calibrated daily."*

And on the buffer specifically:

> *"higher beta keep a buffer of 15% price move for stop loss and watch until price actually
> moved substantially."*

> *"My goal is to systematically exit in a controlled manner into strength."*

Three things follow, and they are the design constraints:

1. **The stop protects a gain, not an entry.** It is only armed once there is a gain to protect.
2. **Buffer scales with how the name actually moves**, not with a flat percentage.
3. **It recalibrates daily, but can only ever tighten** (see §4).

---

## 2. The pieces

```
SIGMA20      the name's own daily volatility, in PERCENTAGE POINTS PER DAY
k            "sigma-days" — how many typical days of movement the stop tolerates
base         = k × SIGMA20              the raw buffer
m            alpha multiplier, 0.35–1.45 (RSI / velocity / peak-horizon / age)
G            gain on COST, i.e. (price − cost) / cost
buf          = clamp(base × m, lo, hi)  the buffer actually used
StopPrice    = max(prior_stop, HighWater × (1 − buf))
```

### Why `k` in sigma-days instead of a flat percentage

A 15% buffer means completely different things on two names:

| | daily σ | 15% buffer is… |
|---|---|---|
| KO | 1.18pp | **12.7 typical days** — very loose, almost never fires |
| MRAM | 7.24pp | **2.1 typical days** — inside the noise, fires constantly |

So a flat percentage is not one policy, it is 239 different policies. `k` normalises it: *how
many of this name's own days do I let it breathe before I'm out?* That question is answerable
once per name and is stable, which a percentage is not.

**Read `k = 12` as: the name must fall twelve typical days' worth below its high-water mark
before the stop fires.**

---

## 3. THE LOAD-BEARING RESULT — the gain constraint

This is the one piece of the spec that is arithmetic rather than judgment, and it is the reason
the whole thing works. Do not let an agent weaken it.

```
hi = G / (1 + G)
```

**Proof.** With price `P = C(1+G)` where `C` is cost:

```
stop = P × (1 − G/(1+G))
     = C(1+G) × ( 1/(1+G) )
     = C                       exactly breakeven
```

So **any** `buf ≤ G/(1+G)` puts the stop at or above cost. It is a structural guarantee, not a
post-hoc check — the buffer yields to the gain rather than competing with it.

| G | max buffer | | G | max buffer |
|---|---|---|---|---|
| 10% | 9.09% | | 30% | 23.08% |
| 15% | 13.04% | | 50% | 33.33% |
| 20% | 16.67% | | 100% | 50.00% |

**The clamp overrides the band and is never manual.** If `base × m > hi`, then `buf = hi` and
the band is advisory — report `BandClamped = TRUE` so the PM can see it. If `hi` were
overridable the guarantee collapses.

This is also the fix for a real defect found in the 2026-09-11 book: **68 names had stops sitting
below cost.** The gain constraint makes that state unreachable.

**Note the asymmetry of bases:** `G` is a return on **cost**, while position *sizing* in this
book uses **market value** (settled 2026-09-14). Sizing uses market value; stops use cost. Both,
deliberately. Do not "harmonise" them.

---

## 4. The ratchet, and why daily recalibration is safe

```
StopPrice = max(prior_stop, HighWater × (1 − buf))
```

Because of the `max`:

- **σ rises → `buf` widens → `HighWater × (1−buf)` falls → the prior stop is kept.**
  **A volatility spike cannot loosen an existing stop.**
- **σ falls → `buf` narrows → the stop tightens.**

So daily σ drift is **one-directional in effect: it can only tighten.** That is what makes
"calibrated daily" safe rather than jittery.

`SIGMA_USED` is additionally a **5-day median** of `SIGMA20`, not the raw daily figure, so one
event day cannot move the buffer.

---

## 5. When the stop question does not apply at all

The alpha state decides **whether** to place a stop, not how wide it is. (This was tested:
modulating the buffer by RSI/velocity/peak-horizon did **not** rescue names that couldn't clear a
positive floor — 27 cleared vol-only, 27 modulated, 2 rescued, 2 lost. A null result, reported.)

| regime | condition | action |
|---|---|---|
| **ALPHA_AHEAD** | washed + turning + peak horizon still live | **NO STOP.** The widest buffer is the absence of an order. The gain is small by construction and a stop here taxes a thesis that hasn't played out. Carry `HighWater` forward. |
| **ALPHA_WORKING** | the normal case | buffer + ratchet |
| **ALPHA_SPENT** | RSI ≥ 80, peak expired, or RS decay | tighten to harvest: `m = min(m, 0.70)` |
| **UNPROTECTABLE** | `lo > hi` | **no order**, and flag it |

---

## 6. ⚠ THE UNIT ERROR — fix this before implementing anything

**Confirmed 2026-09-14.** The spec's constants are scaled against a sigma **6.30× too small**
(the factor is `100/√252`).

`input/liquidty.tsv`'s `Volatility` column is an **annualised fraction**, not daily percentage
points. Decisive test against names whose volatility is independently known:

| | `Volatility` | read as annualised | read as daily |
|---|---|---|---|
| KO | 0.1879 | **18.8% — correct for KO** | 0.19%/day → 3.0% ann, impossible |
| JNJ | 0.1903 | 19.0% ✓ | — |
| MSFT | 0.3252 | 32.5% ✓ | — |
| TSLA | 0.4743 | 47.4% ✓ | — |
| AXTI | 1.5345 | 153% ann → **9.67pp/day** | — |

**The spec read it the other way round.** Two places prove it:

- §7.4's worked case: *"AXTI at G = 12.66%, σ = 1.53. Even k = 8 gives 12.3%"* — that is
  `8 × 1.5345`, treating an annualised fraction as daily pp.
- §7.1's band provenance (AXTI 9.8, POET 10.5, NVTS 11.9, QBTS 12.9, BE 13.0, ASTS 13.5,
  APLD 14.3) is exactly `15 / Volatility` on the same misreading.

**So these spec values are all wrong and must not be used:**

- the band ladder `k ∈ {8, 10, 12, 15, 20}`
- the seed-ladder thresholds `SIGMA_USED < 0.40 / 0.70 / 1.00 / 1.30`
- the §7.4 AXTI worked example
- test case 4 (`SIGMA20 = 1.5 → lo = 0.12`)

**Correct `SIGMA20` from this column as `Volatility / √252 × 100`.** Better: compute it properly
per §3A of the spec (log returns, 20 sessions, Bessel-corrected, non-zero mean, winsorised at
±5 × SIGMA60, 5-day median) once a real price series is available. `liquidty.tsv`'s column is
computed over `DataDays` (median 2,763 sessions ≈ 11 years), **not** 20, so it is a long-horizon
proxy at best — mark any figure derived from it **UNVERIFIED**.

### What the corrected numbers actually look like

`k` implied by the PM's own stated 15% buffer, i.e. `k = 15 / daily σ`, across the 239-name
trading book:

| | k (sigma-days) |
|---|---|
| p10 | **2.51** |
| median | **4.61** |
| p90 | **8.27** |
| range | WVE 1.42 → TRP 12.71 |

So the ladder should span roughly **{2, 3, 4.5, 6, 8}**, not `{8, 10, 12, 15, 20}`.

### The structural problem the unit fix does NOT solve

The spec's noise floor is `lo = max(0.03, 8 × SIGMA20)` — "never put the stop inside 8 sigma-days."
With correct sigma, `8 × σ ≤ 30%` holds for only **138 of 239 names (58%)**. The other 42% get
`lo > hi` at *every* gain level and the spec emits no order.

That is **not** a unit artifact and **not** the `hi_abs = 0.30` ceiling's fault. AXTI genuinely
moves 9.67% a day; eight of those is 77%. For such a name, a stop that is both outside its own
noise and above a 12.66% cost basis does not exist. **UNPROTECTABLE is the honest answer**, and
the guard that produces it is the single most important line in the spec.

But it does expose that the PM's stated preference and the spec's floor disagree:

> **A 15% buffer on a high-beta name is ~2 sigma-days, not 8.**
> MRAM (7.24pp/day) → 2.07 days. ASTS (7.00) → 2.14. AXTI (9.67) → 1.55.

Floor sensitivity, names that can sit outside their own noise under a 30% cap:

| floor | coverage |
|---|---|
| 2 sigma-days | 239 / 239 (100%) |
| 3 sigma-days | 238 / 239 (100%) |
| **4 sigma-days** | **233 / 239 (97%)** |
| 5 sigma-days | 217 / 239 (91%) |
| 6 sigma-days | 195 / 239 (82%) |
| 8 sigma-days *(as specced)* | 138 / 239 (58%) |

**This is the PM's decision, not the agent's.** It is a real trade-off: a lower floor means the
high-beta sleeve gets stops that will sometimes fire on ordinary noise; the current floor means
that sleeve gets no stops at all. There is no setting that avoids choosing. **An agent must not
pick one unilaterally** — present the table and let the PM choose.

---

## 7. How `k` is governed — set once, sticky, auditable

`k` is **the PM's one discretionary input per name.** The engine never recomputes or overrides it.

| event | behaviour |
|---|---|
| symbol first gate-eligible, no `k_band` row | write the seed, `KSource = SEED`, **emit no order that day** — PM reviews the seed first |
| row exists | use it, unchanged |
| PM edits the band | `KSource = MANUAL`, new `SetDate`, effective next run |
| position exited | **keep the row** — a re-entry inherits the band and its reasoning |
| σ regime shift (`SIGMA20/SIGMA60 > 2.0`) | report `VolRegimeShift`; do **not** change the band |

**Why sticky matters:** a buffer that re-derives itself daily cannot be audited, because you can
never separate the PM's judgment from the model's drift. A sticky band can — in six months,
*"which band was this on when it stopped, and was that right?"* has an answer.

`k` is deliberately **not fitted to realised history.** Those lots were exited under discretion,
not under this rule, so fitting to them is circular. Model-based calibration waits until
signal-path history exists.

---

## 8. What to tell an agent, in one paragraph

> The buffer is `k × SIGMA20`, where `SIGMA20` is the name's **daily** volatility in percentage
> points and `k` is a manually-set, sticky count of sigma-days. It is then clamped between a
> noise floor and `hi = G/(1+G)`, which is the arithmetic guarantee that the stop never sits
> below cost. The stop only ratchets up, so daily recalibration can only tighten it. If the floor
> exceeds the ceiling the name is UNPROTECTABLE and you emit no order — that guard is the point,
> not a bug. **The spec's numeric constants are wrong** (annualised vol was read as daily; see
> §6) and must be re-scaled before use. Whether to lower the 8-sigma-day floor is an open PM
> decision — do not decide it.

---

## 9. Open decisions for the PM (do not resolve these as an agent)

1. **Re-scale the k ladder** to sigma-days on corrected units — roughly `{2, 3, 4.5, 6, 8}`.
2. **The noise floor**: keep 8 sigma-days (58% coverage, high-beta sleeve unprotected) or lower
   it toward 4 (97% coverage, more noise-exits)?
3. **`hi_abs = 0.30`** — Claude's choice, never PM-derived. Keep, raise, or drop it?
4. **Seed-ladder direction.** As written it *lowers* `k` as σ rises, trading noise-exits for less
   give-back on wild names. That is a stated preference, not a derivation — invert it if the PM
   would rather hold through the chop.
5. **`cluster_cap = 8%`.** Related quantified risk: per-name stops are individually sound and
   collectively correlated — **$64,176 = 12.7% of the trading book would fire on one −5% index
   day.**
6. Plus four more in spec §15.

---

## 10. Correction history on this mechanism — cite these, they were all real

An agent working here should expect to be wrong in these specific ways:

- **"The floor/buffer collision requires +35.3%"** — false premise. In the PM's method **the
  floor is an OUTPUT** of (price, cost, buffer), not an input. Retracted.
- **Merrill `TrailingStopLimit`** — argued from documentation; the PM's account of their own
  broker (*"not dynamic/rolling % on spot price. It is a fixed stop and limit price $ based on %
  of spot price order was placed"*) takes precedence. The spec was rebuilt on plain stop-limits
  at explicit prices so it depends on nothing unresolved.
- **"`hi_abs = 0.30` is the binding constraint"** — wrong diagnosis (2026-09-13). The
  unprotectability is real, but its cause is that 8 sigma-days is enormous for high-σ names, not
  the ceiling. Corrected 2026-09-14.
- **The sigma unit error in §6** — introduced by Claude when writing the spec, caught by Claude
  a day later. It invalidated every constant in §7.1.

**Nothing in this file is an order or a recommendation to trade. Levels, sizes and every exit
remain the PM's.**
