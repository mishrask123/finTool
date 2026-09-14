# HANDOVER — alpha++ long book, Claude agent briefing

**Written:** 2026-09-14 · **By:** the outgoing Claude session
(`https://claude.ai/code/session_01Di9HUW95Ts95FeknYvvpKb`)
**Read this before touching anything.** It is written for a Claude agent picking up cold.

---

## 1. Who you are working for, and the situation

**Saman Mishra**, PM of a systematic long-equity book called **Alpha++**. Roughly 400 names
targeted, ~241 held. Rotational, not buy-and-hold. Breadth is the engine.

**The constraint that shapes everything:** the PM is away from their home PC
**2026-09-06 → 2026-09-20** with only an **iPad and broker web portals (Merrill, Schwab)**. The
Windows toolchain — `ps\recon`, `calc_size`, `worksheet_set`, the C#/.NET pipeline — **cannot
run.** You are the substitute for the parts of that pipeline that can be done by reading files
and reasoning. You are not a substitute for the parts that need live market data.

**Book as of 2026-09-11** (`broker/positions_20260911.csv`, 241 rows):

| | |
|---|---|
| equity | $534,643.12 |
| positions | 241 |
| unrealized | −$3,540.54 (−0.66%) |
| **hedge OXY + OXYWS** | **$30,141 (5.64%) — NOT FOR TRADE** |
| **trading book** | **$504,502 across 239 names, weighted beta 1.54** |
| money accounts | $573,013.62 (cash −$8,524.39) |
| **total** | **$1,099,132.35** |
| ST gain/loss | −$14,487.37 |
| LT gain/loss | +$10,946.83 |

---

## 2. YOUR LANE — the hard rules

These come from explicit PM instruction on 2026-08-28 and have been reinforced since. Violating
them is the fastest way to lose usefulness.

**You do: due diligence, and trailing-stop-loss analysis. That is the lane.**

1. **NO sizing.** Do not propose position sizes.
2. **NO pricing.** Do not propose limit prices or entry levels.
3. **NO order-building** unless explicitly asked — and then **once**, without iterating.
4. **Exits are the PM's, always.** Never recommend, push, or trigger a sell. You may *observe*
   that a stop was breached. You may not conclude it should be acted on.
5. **Never use market cap as a risk lens.** The book's risk lenses are **liquidity** and
   **geography**. Market cap is explicitly rejected.

**What you SHOULD volunteer:** data defects, arithmetic consequences, cluster/concentration
facts, and anything where your own earlier statement was wrong. The PM values a correction more
than a clean story. Several of the most useful contributions in this session were self-corrections.

**Source discipline:** quote verbatim, cite file and row, and say **UNVERIFIED** rather than
guessing. Never restate a search snippet's price as live.

---

## 3. The doctrine and its conventions

- **Sizing:** SMALL = **$4,000** (raised from $2,500 on 2026-09-13 as invested capital rose).
  HALF = $2,000.
- **"Add X to $Nk" means target MARKET VALUE, not cost basis.** Settled by the PM 2026-09-14.
  `room = $Ncap − current_market_value`. The cap is target *exposure*, not a capital-at-risk
  budget, so a position that has fallen gets topped up **more**. Cost basis survives in exactly
  one place: the gain constraint `hi = G/(1+G)`, where `G` is a return on cost by definition.
  **Sizing uses market value; stops use cost.** Do not re-raise this per name.
- **Short-interest gate: days-to-cover against DVOL, not raw short %.** The working threshold is
  **DTC ≤ 12.70**, set by STOK having been passed at 12.70.
- **Position age:** 100 days is **not** a hard gate. It is discretionary, used as a check on drift.
  For names over ~100 days the PM cuts under human discretion. Do not treat it as a rule.
- **The 7-step DD gate:** memo → `short_aggregate` (% of FLOAT) → `otc_aggregate` → 13F →
  `recon_order` RSI → raw filing → **live broker screen**. Step 7 is the PM's veto and you cannot
  perform it. Everything you produce is pre-step-7.
- **Grounding is the PM's job, not yours.** You screen; they ground. Say so explicitly every time
  you hand over a list.

---

## 4. THE DATA — and everything known to be wrong with it

Local working copy at **`/home/user/gdrive/`** (mirror of the Drive `quantbot/` tree). It is
**not** a git repo and is **ephemeral** — the container is reclaimed. Anything worth keeping goes
to Drive or to git.

```
input/   short_aggregate.tsv     settle 2026-08-14
         otc_aggregate.tsv       asof 2026-09-02
         eod_price.tsv           SINGLE timestamp 2026-09-05 01:48:24, 7,705 rows
         equity_px.txt           OHLC all == Close (a snapshot, not bars)
         liquidty.tsv            Symbol Name AsOfDate Close MarketCap AvgVolume20
                                 DollarVolume Beta Volatility DataDays  (DataDays median 2,763)
         demand_converge.tsv     asof ~2026-09-07, 6,151 rows — the main screen input
         early_alpha.tsv · equity_meta.txt · etf_meta.txt
pnl/     20260904.tsv            14:32 ET intraday snapshot, 452 MERRILL lots
broker/  open_orders.tsv         21 GTC orders
         positions_20260911.csv  241 rows, Claude-parsed from a pasted export
poc/20260902/mm_prealpha/invest.tsv   111 rows — ALL asofdate 2026-08-31
poc/20260902/mm_micro/predict.tsv     560 · mm_micro/etf.tsv 893
poc/20260903/ALPHA.run.tsv            2,111 rows, 29 ADDRESSED
poc/20260902/ALPHA.run.tsv            3,105 rows, 44 ADDRESSED
report/  pnl_realized_lots.tsv   1,107 usable lots, 344 symbols
llm/     worksheet.archive.zip   1,144,648 B → 186 files, 24 dates, 13 types
temp/    scratch_pad.txt         the PM's home-PC working memory — READ IT, it carries intent
tablet/  the deliverables written for this trip
```

### Defects you must know about

1. **`RealizedPnlPct` in `report/pnl_realized_lots.tsv` is BROKEN.** It produces absurd values
   (SMH +1.5% on $13,200 of profit, implying $880K of cost). **Always recompute** as
   `RealizedPnl / AcquisitionCost`. That gives sane numbers (median winner +15.3%, max +315.8%).
2. **`poc/20260902/mm_prealpha/invest.tsv` is 4 sessions stale** — every row reads
   `asofdate 2026-08-31` despite the `20260902` folder. **27 of its 111 rows had already traded
   through their own 20-day target.** Pre-screen rule: reject anything trading above
   `pred_target_px_20d`.
3. **`invest.tsv` columns with zero information:** `dd` and `smooth` are constant across all 111
   rows; `ear` is constant on 108/111. The entire liquidity leg (`liquidity`, `liq`,
   `cross_otc_x_liq`, `cross_trend_x_liq`) is **0 on 111/111**.
4. **`otc = 0.0000` means UNMEASURED, not neutral.** 14 of 66 screened names had no row at all in
   `otc_aggregate.tsv`.
5. **All local price files are single-day snapshots.** `eod_price.tsv` has one timestamp;
   `equity_px.txt` has OHLC all equal to Close. **You cannot compute RSI, velocity or distance
   locally.** The series lives in `price.zip` (481 MB), which was skipped. Any RSI/VEL/DIST you
   use must come from `demand_converge.tsv`.
6. **`demand_converge.C_DTC` is NOT an independent measurement.** It reproduces
   `short_aggregate.latest_days_to_cover` **exactly** on every name checked (SPIR 6.25, TGTX
   12.59, CERS 5.07, CRMD 11.05, MRAM 2.44). So the whole short-interest leg rests on **one**
   source settling **2026-08-14** — about 30 days stale. Apparent cross-file agreement is
   propagation, not confirmation. **Check this pattern before claiming any two files corroborate
   each other.** Price columns, by contrast, are only *partly* propagated (SPIR and CERS match
   exactly; TGTX 55.99 vs 56.71 and CRMD 8.43 vs 8.47 differ).
7. **`liquidty.tsv`'s `Volatility` is computed over `DataDays`** (median 2,763 sessions ≈ 11
   years), **not** 20, and the column's definition is undocumented. Using it as a proxy for a
   20-day sigma is an approximation — **mark it UNVERIFIED**.
8. **Model churn is severe.** `ALPHA.run.tsv` passed 44 names on Wednesday and 29 on Thursday,
   with only **BEKE and RXRX** on both — 93% overnight turnover. `emerging`'s `Score` column is
   dead (17 of 29 exactly 0.0). `mean_rev` prices are **frozen on repeats** (FORM printed
   101.69 / Comp 83.37 on three separate days). `micro` produced zero output on 3 of 5 days.

### Egress-blocked domains

`finance.yahoo.com`, `stockanalysis.com`, `www.cnn.com`. Search snippets routinely restate stale
closes as if live. **Prices come from the broker screen, never from a snippet.**

---

## 5. Where the work stands right now

### The $50,000 deployment tranche (2026-09-13 → open)

PM holds $600,000 in money market, deploying $50,000 into deep-discount alpha++ names.
**10 orders placed, $16,347.95. $33,652.05 uncommitted.** Full itemised record:
**`quantbot/tablet/buy_decisions_20260913_rev2.md`** (id `1ltqwRAIn1hKfql8lXszzRr9yr8I3gZhU`).

Every order is a **GTC limit parked below market**, so the FOMC acts as a fill mechanism rather
than a timing risk. That structure is the PM's own, from the RKLB order — and it was better than
the "wait until Thursday" advice this session first gave. Placed dollars run **weighted beta
2.94**, **52.1% Technology**, **67.9% in names with beta > 3**.

**Two order-level flags still unresolved** (only the PM's live screen settles them):
- **COHU $53** sits *above* both local references (+4.5% vs the 09-04 close, +15.3% vs 09-07) —
  it fills at the ask, not on weakness.
- **ENTG $135** *straddles* them (−2.7% vs 09-04, +3.3% vs 09-07) — genuinely ambiguous.

**13 held names still awaiting the PM's grounding:** ALT, MTSI, BAND, ACMR, NOK, PUMP, MRP, EE,
TRU, SUPV, ASTS, HIMX, LRCX. Eight are Technology, which would concentrate the tranche further;
the low-beta diversifiers among them are MRP 0.78, EE 0.45, TRU 0.95, PUMP 0.94.

**10 names passed grounding but carry no price:** INDI, SIDU, TGTX, CERS, CRMD, ROOT, EVGO, SG,
EZPW, ANDG.

### The gain-protection stop spec

**`quantbot/tablet/spec_gain_protect_buffer_rev2.md`** (id `1N5o-GQ9qVuB3ebRGcu9dgB7mXEKqpnTO`,
26,058 B) — canonical. Rev 1 is renamed `..._rev1_SUPERSEDED.md`. Git copy at
`spec/spec_gain_protect_buffer_rev2.md`.

The load-bearing result, and the thing to understand before editing anything:

```
hi = G / (1 + G)                 THE GAIN CONSTRAINT
With P = C(1+G):  stop = P(1 − G/(1+G)) = C exactly.
So any buf ≤ G/(1+G) structurally guarantees the stop never sits below cost.
```

The clamp:

```
lo  = max(0.03, 8 × SIGMA20)     never inside 8 sigma-days
hi  = min(0.30, G / (1 + G))     hi_abs = 0.30
buf = clamp(k × SIGMA_USED, lo, hi)
lo > hi  →  Regime = UNPROTECTABLE, Action = NONE   (no order)
```

`SIGMA20` is in **percentage points** (test case 4: `SIGMA20 = 1.5` → `lo = 0.12`).

**`k` is manual, banded, set once.** Its provenance is the PM's own stated "15% buffer on
high-beta", which implies k ≈ 10–14. It is **deliberately NOT fitted to realized history** —
that would be circular, because those lots exited under discretion.

**Ratchet asymmetry:** because `StopPrice = max(prior, HighWater × (1−buf))`, a sigma *rise*
cannot loosen an existing stop. Sigma drift can only tighten.

**Alpha regimes:** ALPHA_AHEAD (washed + turning + PeakT live → **no stop at all**),
ALPHA_WORKING (buffer + ratchet), ALPHA_SPENT (RSI ≥ 80 / PeakT expired / RS decay →
tighten-harvest), UNPROTECTABLE.

#### THE OPEN FINDING — read this before anyone implements the spec

`8 × SIGMA20` exceeds the `hi_abs = 0.30` ceiling whenever daily sigma passes **3.75pp**. Then
`lo > hi` holds **unconditionally — at every gain level** — and the spec refuses to write a stop.

**That is an estimated 101 of 239 trading-book names (42%).** WVE 10.58pp, AXTI 9.67, POET 9.00,
NVTS 7.97, BW 7.97, BFLY 7.95, CIFR 7.40, QBTS 7.31, BE 7.25, ASTS 7.00, FLY 6.98. Of the 10
orders just placed, only **VTS** (arms at +19.4%) and **ETOR** (+35.9%) can ever carry a stop.

**Why it matters:** the framework was designed around the gain constraint, which is arithmetic.
But for 42% of the book the binding term is instead `hi_abs = 0.30` — **a number Claude chose,
not one the PM derived** — and it binds hardest exactly where the PM said they wanted a 15%
buffer. That inverts the design intent. **Logged as an open decision for spec §15. Do not "fix"
it unilaterally.** (The sigma population count is a proxy and UNVERIFIED per defect 7; the
structural result is arithmetic and holds regardless.)

Spec §15 carries nine open PM decisions, chiefly the seed-ladder direction and `cluster_cap = 8%`.

### The bounce-back screen (2026-09-13)

Hard gates: `DVOL ≥ $5m` · `DTC ≤ 12.7` · not micro-SELL · `RSI < 35` · `VEL ≥ 50` · room to cap
≥ $1,000. 274 of 6,150 names passed.

```
score = 0.30·VEL + 0.22·WASH + 0.20·SUPPORT + 0.14·CONV + 0.08·FUEL + 0.06·DIST
WASH    = (35 − RSI)/35 · 100
SUPPORT = 40·(A_NetFlow>0) + 30·(A_NewCt>A_ClosedCt) + 30·('A' in Flags)
FUEL    = min(100, C_Short(%flt)·5) if C_Short(%flt) ≥ 3 else 0
CONV    = min(100, ConvScore/200·100)
```

**Two lessons baked into it:**

1. **Require the A leg, not just the D leg.** A leg filter (held ≥2 legs or live DIST; new ≥3
   legs) dropped 12 of the previous day's 24 names because their only leg was **D**. Demand
   turning with no 13F accumulation under it is *a turn without a bid*.
2. **`FUEL` is broken and known to be broken.** It reads short-interest **magnitude only** — not
   `C_ShortChg(%)` (growing or shrinking) and not days-to-cover (how fast it can clear). So VTS
   (covering −5.7% on an 11.88-day cover — real fuel) and AIRJ (building +2.0% on a 2.66-day
   cover — no fuel) scored identically. **Candidate fix, offered and not yet taken up:** weight
   `FUEL` by `−C_ShortChg(%)` and by days-to-cover. The PM was told this would re-rank the 13
   remaining names and that the re-rank is their call.

---

## 6. MISTAKES THIS SESSION MADE — do not repeat them

Listed because each one cost credibility and each has a transferable lesson.

| what happened | lesson |
|---|---|
| **WEN** — recommended it on a perfect factor profile (R:R 2.22, ConvScore 268, A+B+C, DTC 3.9). Grounding found Trian had shelved the take-private, FY outlook withdrawn, same-restaurant sales −7%. The `OTC_SPIKE` was dated **four days after** the collapse. | **The factor files cannot distinguish accumulation from liquidation.** Never present a screen result as a recommendation. |
| **BAND** — reported its stop as breached and read it as a finding. The PM's own scratch pad said *"4/4 held; hold the accumulation, do not cut."* BAND then went **+29.9% in five sessions**. | **Read `temp/scratch_pad.txt` first.** A breached stop on an accumulation the PM marked do-not-cut is an observation, not a finding. |
| **BAND/CRDO** — called them "broken stops." | They were **triggered** stops. The stops sat correctly below spot; price traded through them. Diagnose before labelling. |
| **OXY** — scored the hedge as an 11× sizing breach and led a report with it. PM: *"Oxy and oxyws are hedge not for trade."* | **Carve the hedge out of every book statistic.** Correct figures are 57 positions / 40.5% of the *trading* book; trading-book beta **1.54**, not 1.43. |
| **RKLB insider selling** — called "110 sales, 0 purchases" *"the cleanest signal available."* It was a **Rule 10b5-1 plan** (Beck via Equatorial Trust, adopted 2026-03-27). | It was the *loudest* signal, not the cleanest. Ground insider data before characterising it. |
| **`RealizedPnlPct`** — divided by 100 and produced absurdities. | Recompute from `RealizedPnl / AcquisitionCost`. See defect 1. |
| **Null-sort bug** — used `−1e18` as the missing-value sentinel on a descending sort, so nulls sorted to the **top**. | Use `+1e18` for descending sorts. |
| **"Floor/buffer collision"** — claimed a 15% floor plus a 15% buffer required +35.3%. | The PM corrected it: **in their method the floor is an OUTPUT** of (price, cost, buffer), not an input. Retracted. |
| **Merrill `TrailingStopLimit`** — argued from documentation. PM: *"not dynamic/rolling % on spot price. It is a fixed stop and limit price $ based on % of spot price order was placed."* | **Accept the PM's observation of their own broker over the docs.** The spec was redesigned around plain stop-limits at explicit prices so it depends on nothing unresolved. One call to Merrill would settle it; it hasn't been made. |
| **Claimed MRAM's DTC was "independently corroborated" across two files.** | It wasn't — see defect 6. **Verify that two sources are actually independent before saying they agree.** |
| **Alpha-modulation null result** | Modulating the buffer by RSI/VEL/PeakT did **not** rescue the negative-floor group (27 clear vol-only, 27 modulated, 2 rescued, 2 lost). Reported honestly and reframed: **the alpha state decides whether the stop question applies, not the buffer size.** Null results are worth reporting. |
| **"Wait until Thursday" on RKLB** | The PM's own answer — a GTC limit at $59, 6.3% below the mark — was strictly better, because it solves the FOMC timing problem without needing a view on Wednesday. **Say so when the PM's answer beats yours.** |

---

## 7. Tooling gotchas

- **Google Drive MCP:** `read_file_content` is **LOSSY**. `download_file_content` is byte-exact
  base64. **`update_file` CANNOT replace content** — only title and parentId. To revise a
  document: create a new file, then rename the old one `..._SUPERSEDED.md`. That is why the spec
  and the buy record both have `_rev2` names. Verify uploads by comparing the returned
  `fileSize` against the local `wc -c`.
- **Git:** work on branch **`claude/new-session-8id6my`** in `mishrask123/finTool`. Earlier
  session work sits on `tactical`. Commit messages end with the attribution lines the harness
  supplies.
- **`/home/user/gdrive/` is ephemeral and not a git repo.** Deliverables must be pushed to Drive
  *and* copied into `spec/` in the repo.

---

## 8. Open items, in rough priority order

1. **`mishrask123/finTool` is a PUBLIC repo** holding positions, realized P&L, stops, live order
   IDs and 50+ decisions. **Flagged to the PM roughly seven times across this session with no
   decision.** Raise it once more, then let it be — it is their call, not yours.
2. **STX** ($4,981, second-largest single name) and **FN** have **no stop at all.**
3. **Schwab-401K stop-parity gap:** DAC 5%, ITUB 7%, PFE 7%, SGI 5%, VALE 6%.
4. **Four live `TrailingStopLimit` orders unadjusted** while the PM is out of office — PBR 7%
   (+19.98%), DAC 5% (+15.21%), ITUB 7% (+13.55%), ALT 5% (+11.22%). Given the PM's own account
   of how the order type behaves, these protect *entry*, not gain, if left static.
5. **ALT** has 294 sh — the entire position — under open stops in ROTH 1 (98 sh, `VVO-254`) and
   IRA 2 (196 sh, `VVX-248`). **Any shares added there are unprotected until the order quantity
   is extended.** ALT is still on the ungrounded add list.
6. **PBR** — hedge or trading book? Undetermined. It matters for every book statistic.
7. **Spec §15's nine open decisions**, chiefly the seed ladder and `cluster_cap = 8%`, plus the
   `hi_abs` finding in §5 above.
8. **Cluster risk, quantified and unaddressed:** per-name stops are individually sound and
   collectively correlated. **$64,176 = 12.7% of the trading book would fire on one −5% index
   day.**
9. **Biotech catalyst calendar** — a deferred separate project for the week of 2026-09-21. The PM
   said Paula's calendar is the right instrument for biotech rotation timing. Note that TGTX,
   CERS and CRMD passed grounding *before* that instrument exists, into a Healthcare sleeve
   already at 35 names / $83,185 / 16.5% of the trading book with 27 of 35 negative.
10. **Whether "Batch A" was actually placed.** All nine names are in the book, but the scratch pad
    says deferred. Unresolved.

---

## 9. How to be useful here

The PM is fast, technically fluent, and does not want to be managed. What has worked:

- **Lead with the number that changes the decision**, then the caveat. Not the reverse.
- **Show the arithmetic.** They check it, and they have caught errors.
- **Volunteer defects in your own output.** The `FUEL` blind spot and the `hi_abs` finding were
  both self-reported and both were received well.
- **Do not soften a correction and do not over-apologise.** State it, fix it, move on.
- **Never let a list imply a recommendation.** Say "for you to ground" every time, because it is
  true every time.
- **Log everything** to `decisions_20260907.md` in the repo, and push. That file is the working
  record across sessions and is at 50+ entries.

---

*Companion documents, all in `quantbot/tablet/`: `buy_decisions_20260913_rev2.md` (the live
tranche record), `spec_gain_protect_buffer_rev2.md` (the stop framework),
`PREALPHA_111_review.md`, `TUESDAY_20260908_card.md`, `decisions_20260907.md`. The PM's own
working memory is `temp/scratch_pad.txt` — read it before forming a view on any held name.*

**Nothing in this file is an order or a recommendation to trade. Levels, sizes and every exit
remain the PM's.**
