# PM decision log — 2026-09-07 (Labor Day, market closed)

Decisions recorded the turn they were made ([[reference-worksheet-set]]).
`worksheet_set.cmd` cannot run remotely — fold this into the worksheet at the PC.
Source universe: `poc/20260902/mm_prealpha/invest.tsv` (asof Mon 08-31, 111 names).

## PM DECISIONS

| Date | Symbol | Decision | Note |
|---|---|---|---|
| 2026-09-07 | ETSY | **PASS** | PM call. Was the best-supported name in the filtered cut (R:R 4.0, DVOL $226M, beta 1.17, grounded 09-04). Passed anyway. |
| 2026-09-08 | **IESC** | **BUY — HALF** | PM call; PM doing own DD. Claude had said PASS on internal contradictions (otc factor +2.4432, highest in 111 and 2.5x next, vs OTC flow 0.39x and the row's own reason field saying OTC:0.2520; price -0.2713 and short -0.6400 both negative; liquidty mktcap $6.43B vs Merrill $12.85B = 2x break; PeakT 2d passed). Upside +22.5% to target 395.21. **Stop 221.47 = -31.3%, a genuine catastrophe floor at beta 2.99, sits 31% above the 52wk low 168.47.** Profitable: EPS 11.25, P/E 28.67, 21% below 52wk high, short 6.79% d2c 4.16 covering, no realized history. |
| 2026-09-08 | **PINS** | **BUY — HALF** | PM call, overrides Claude PASS. Claude view was PASS: OTC_SPIKE with `otc` factor -0.0668 (negative, largest in row), OTC flow 0.88x avg ($154.3M vs $175.9M), PeakT 5d passed, prob 0.70 / Cons 0.40 weakest in file. PM took it anyway on risk shape: R:R 1.68 (+10.7% target 22.59 vs 6.4% stop 19.10), DVOL $194M, beta 0.90, d2c 3.26 with short -13.3% covering, BofA target $28.00 (+37%) and +20.65% 3yr growth, 47% below 52wk high, no realized history. **STOP 19.10 CONFIRMED USABLE** — 6.4% at beta 0.90, sits 38% above the 52wk low 13.84. No re-strike needed. |
| 2026-09-08 | STRL | **PASS** | Claude rec. Target 486.04 vs Fri 486.49 = upside -0.09%, target met. PeakT 4d passed. OTC 0.91x fading, price -0.1019 and short -0.1008 negative. Note: harvested 6 lots 08-04->08-17 @ 520.00 -> 584.99, +$390 (+12.5%) in 13d; now 16.8% BELOW that exit — a re-entry lower, but not on this signal. |
| 2026-09-08 | SGML | **PASS** | RE-CHASE. Held 3 lots, all exited 2026-08-10 @ 11.67 (net -$74.53 on $1,825, -4.1%); Fri close 12.39 = +6.2% ABOVE own exit. R:R 0.39 (+7.1% vs 18.0% stop). Not in otc_aggregate at all (VOLUME_SPIKE, premise intact: price +0.394, short +0.379). Broker data reconciles exactly (mktcap $1.39B, short 3,024,804 both match). 49% below 52wk high, +168% off low. |
| 2026-09-08 | REAX | **PASS** | Corrupt data. predict.tsv target 197.69 on an $18.67 stock (+996.5%). Stop 8.24 is 47% BELOW the 52wk low 15.50 = unreachable. liquidty mktcap $4,069M vs Merrill $409M (10x); short_aggregate 37.5M sh vs Merrill 3.75M (10x, and exceeds the 21.9M shares outstanding). R:R 0.06. |
| 2026-09-08 | BRBR | **PASS** | PM call. Gate fail x4: DVOL $29M, beta 0.01 off-mandate, OTC 0.24x fading, otc attribution NEGATIVE. |
| 2026-09-08 | TMC | **WATCH** | PM call. Best remaining setup: 61% below 52wk high, +31% off an Aug low, price factor +0.4111 on a VOLUME_SPIKE (premise intact), PeakT 24d, clean slate (0 realized lots), CLEAR on all gates. Held back on R:R 0.95 nominal / ~0.6 at a beta-appropriate 15% floor (beta 3.28). Not bought, not passed. |
| 2026-09-08 | XMTR | **PASS** | PM call. Gate fail: OTC_SPIKE flow 0.47x, otc attribution NEGATIVE, R:R 0.3. |
| 2026-09-08 | QURE | **PASS** | PM call. Gate fail: d2c 9.8 trapped, beta 0.23 off-mandate, R:R 0.7. No realized history (clean slate, not a re-chase). |
| 2026-09-08 | KD | **PASS** | PM call. Gate fail: OTC_SPIKE with flow 0.02x — effectively dead flow. R:R 0.7. |
| 2026-09-08 | VSEC | **PASS** | R:R 0.18 (+2.1% target vs 11.7% stop) — worst remaining. PeakT 9d = peak is today. OTC_SPIKE flow 0.89x fading. 3 of 4 factors negative. prob 0.69 / Cons 0.44 lowest in set. P/E 75. |
| 2026-09-08 | LEU | **PASS** | PM call. Gate fail: d2c 9.3 (trapped), otc attribution NEGATIVE, R:R 0.2 (+2.0% vs 11.4% stop). |
| 2026-09-07 | ABCL | **PASS** | 52wk-high veto: 11.43 vs high 12.58 = 9% below, after +316% off the low. R:R 0.3, PeakT 9d = peak now, loss-making. Reverses my batch-1 "live case" read, which was made without the 52wk range. |
| 2026-09-07 | MP | **PASS** | PM call. Gate fail: OTC_SPIKE with flow 0.82x average. R:R 0.3 (+4.5% vs 13.5% stop), beta 2.32, DVOL $332M, d2c 3.5, PeakT 18d. |
| 2026-09-07 | FN | **PASS** | PM call. Signal weak: dominant factor `short` -0.3434 (negative), R:R 0.3 (+5.2% target vs 15.6% stop). Already held 4 sh @ 413.80 = $1,629 (-1.9%), lots 8/31 off this same signal — not proven, no top-up. Best business in the file (EPS 13.05, P/E 31.22, DVOL $404M, short 3.28%/d2c 1.6, 46% below 52wk high) but that is a quality thesis, not this signal. |
| 2026-09-07 | AGYS | **PASS** | PM call. Matches batch-1 rec and gate: DVOL $27M, beta 0.52 off-mandate, OTC flow 0.31x average. |
| 2026-09-07 | TDC | **PASS** | PM call. Agrees with gate: OTC_SPIKE with flow 0.60x average. R:R 1.5, beta 1.30, DVOL $55M, d2c 4.9. |
| 2026-09-07 | TPB | **PASS** | PM call. Confirmed: DVOL $20M, beta 0.62 defensive = off-mandate, d2c 6.78. |
| 2026-09-07 | STOK | **PASS** | PM: high shorts. Confirmed extreme: 12.98M sh short, **d2c 12.70** on $26M DVOL (~13 days of full volume to unwind), 82% of its own max short, short worth ~20% of mktcap. Signal weak too: OTC flow 0.78x avg, price factor -0.1097. |
| 2026-09-07 | TNDM | **PASS** | OTC_SPIKE signal with `otc` attribution -0.2734 (negative) and OTC flow 0.65x average. Ungrounded, no predict.tsv cross-check. Squeeze (15.45%, covering) and BofA $25 target are real but are not what the signal fired on. |

## OPEN — put to PM, not yet decided

| Symbol | State |
|---|---|
| BFLY | Only one of the three whose stated engine is actually firing (OTC 1.45x, otc attribution +0.4359, strongest in file). HALF discussed. Sizing OK'd as a class; stop width unresolved — file stop 4.2% (7.05) is unusable at beta 3.41, use ~15% floor (~6.26). No PM decision yet. |
| **NO STOP on held names** | STX (7 sh, $5,945) and FN (4 sh, $1,629) both have zero open orders. Neither is protected. |
| STX | Held 7 sh (~$5,945, avg 819, +3.7%), 2.4x standard size, NO STOP in place. Add / floor question open. |

## Claude recommendations (NOT decisions — batch 1 of the 111)

| Symbol | Rec | Basis |
|---|---|---|
| ABCL | live case | +5.8% to target, PeakT 9d, short covering -14.4%, micro BUY. DVOL $101M. |
| ACHR | PASS | peak passed (4d), +3.1% left, OTC flow halved vs average |
| ACLS | PASS | peak passed (5d), +1.5% left vs 12.5% stop, DVOL $33M |
| AEHR | PASS | target exceeded, peak passed, micro says -27.8%, beta 5.50 |
| AGYS | PASS | beta 0.52 off-mandate, DVOL $27M, OTC flow down ~70% — **confirmed by PM 09-07** |

## Full-gate screen of the clean 32 (2026-09-07)

Gates: d2c>=8 trapped | DVOL<$30M | beta<0.8 off-mandate | OTC_SPIKE with flow <1.0x |
negative `otc` attribution | stop too tight for beta.

**5 of 32 survive: FLNC, TMC, LASR, FN, ABCL.** FLNC and LASR carry micro SELL, leaving
**TMC, FN, ABCL**. None grounded; none with R:R > 1.0.

BFLY fails on stop width (4.2% at beta 3.41); re-struck at a ~15% floor its R:R is 1.4,
no better than the survivors.

All eleven hand-screens (ETSY, TNDM, STOK, TPB, TDC, AGYS, FN, MP, ABCL, LEU, VSEC) came back PASS — zero
disagreements between PM judgement and the gate set. FN was CLEAR on the gates but failed
on signal quality (negative dominant factor, R:R 0.3), which the gates do not capture.

## Note on Claude's DD reliability (PM, 2026-09-08)

PM: *"let me dd myself yours is not reliable."* Context: 20 of the first 21 calls were PASS.
Claude was defaulting to PASS whenever a number could not be verified, which converts every
data-quality problem into a veto and makes the output useless for finding entries. Flag the
uncertainty, state which way it cuts, and let the PM weigh it — do not treat unverifiable
as disqualifying by default.

## Standing data-integrity items

- **BAND / CRDO / ASAN** — `stop_loss_px` above Friday's close; fire instantly if placed as written.
- **BFLY** — same class of problem, not yet inverted: 4.2% stop at beta 3.41.
- `pnl/20260904.tsv` is a **14:32 ET intraday snapshot**, not the close; its PnL understates.
- `limit_px` is the 20d TARGET, not an entry limit (identical to `pred_target_px_20d`, 111/111).
- **REAX row is corrupt**: 10x share count and mktcap vs broker, short > shares outstanding,
  micro target 197.69 vs price 18.67 (+996.5%), stop 47% below the 52wk low.
- `RealizedPnlPct` in `report/pnl_realized_lots.tsv` is 100x too large (+34.2% shows as 3420.00%).
- **LASR is a re-chase**: bought 08-03 @ 65.90, cut 08-19 @ 48.54 (-26.3%, 6 lots), now 40.06.

---

# Tuesday 2026-09-08 — session 2

## Longs placed by PM (half size, limit orders)

| Sym | otcFac | OTCx | R:R | Up% | Stop | Rsk% | Stop in vol-units | Beta |
|---|---|---|---|---|---|---|---|---|
| BFLY | 0.4359 | 1.44 | 5.14 | +21.5 | 7.05 | -4.2 | 3.3 | 3.41 |
| PINS | — | — | — | — | 19.10 | -6.4 | 12.3 | 0.90 |
| IESC | 2.4432 | 0.39 | 0.72 | +22.5 | 221.47 | -31.3 | 34.1 | 2.99 |

PM took all three at HALF ($1,250) on limit orders. Claude gave no sizing and no limit price.

## 22. WEN (Wendy's) — Claude: BUY candidate, best of the 49 undecided

Only name in the residual set that clears every gate Claude can check offline.

- `invest.tsv` row: `spot=8.2715 stop=7.7304 tgt20d=8.6942 prob=0.812083 src=OTC_SPIKE`
- `reason: PeakPct:5.11% Holding:-0.0039 OTC:0.0354 Short:0.0000 Mixed:0.0204` · PeakT **7**
- vs Friday close 8.03 → **Up +8.3% / Rsk -3.7%, R:R 2.22**
- stop 7.73 sits **6.2 vol-units** below the close — robust, not a noise stop
- `liquidty.tsv`: **Beta 0.35** — lowest in the whole 66-name set; the book is full of β 3-4
- `demand_converge.tsv`: **ConvScore 268, flags A+B+C** (13F + OTC + short legs all converging), RSI 43
- `short_aggregate.tsv` settle 2026-08-14: 32.5% of float short but **DTC 3.9** (max 8.46), short
  count fell -13.2% vs prior period — passes the PM's d2c gate (STOK was passed at 12.70)
- `mm_micro/predict.tsv` action = **BUY** — micro agrees with prealpha
- DVOL $81M · not held · no realized history · no open GTC order

## 23. BWXT — Claude: second-best, but position already near the cap

R:R 1.88, prob **0.9698** (highest in the set), PeakT **21**, stop 10.6 vol-units (very robust),
short 3.0% of float / DTC 3.23, DVOL $164M. Against it: **already held $2,211**, and convergence is
thin — ConvScore 70, flag **A only** (13F, no OTC/short/demand confirmation).

## 24. SQM — Claude: PASS. Headline R:R is a stop-placement artifact.

R:R 6.93 tops the whole list, but only because `stop_loss_px` 75.25 sits **1.5%** below the 76.43
close = **3.2 vol-units**, the same hair-trigger tier as BFLY (3.3) and OMER (3.2). The ratio is
inflated by a stop inside the noise, not by edge. Also already held $1,919, ConvScore 64, flag D only.

## 25. IT (Gartner) — Claude: WATCH, not buy. Move is nearly spent.

Clean on liquidity (DVOL $208M), beta 0.53, DTC 4.15, stop 13.7 vol-units. But **PeakT:3** — the
model puts the peak 3 days out — and `demand_converge` **RSI 80**. Both say late.

## 26. INBX — Claude: PASS on the short gate.

OTCx 1.50 (2nd highest) and R:R 1.31, but **DTC 14.4** on 38.4% of float. Above the level the PM
passed STOK at (12.70).

## 27. RAMP — Claude: PASS. Same pathology as IESC.

otcFac 0.5242 (7th highest) but **OTCx 0.20** — OTC notional is running 80% below its own 7d average.
The model is leaning on a leg that is currently dead. Upside only +5.6%.

## 28. FDX — Claude: PASS. Nothing is converging.

R:R 1.09 and clean short (DTC 3.2), but **ConvScore 37, no flags** — the lowest convergence of any
name with a positive R:R. It is a large cap with a price target and no demand signal behind it.

## New data-integrity items (2026-09-08)

- **`dd` and `smooth` are constant across all 111 rows** — `dd = "HIGH: Extreme Gap Risk"` 111/111,
  `smooth = "NOISY: Erratic Move"` 111/111. Zero discriminating information. `ear` is 108/111
  `"STRUCTURAL: Factor Driven"`. Three more dead columns alongside the dead liquidity leg.
- **14 of the 66 have no row in `otc_aggregate.tsv` at all** — ABCL BTDR CLVT CRDO FN GCT HLF IREN
  NAMS NVCR QURE REAX SGML TMC. Their `otc` factor of 0.0000 means **unmeasured, not neutral**.
  The "filter out negative otc" screen keeps them in as if they were clean.
- **OTCx** (Claude's, not the pipeline's) = `latest_usd_notional_sum / avg_daily_usd_notional`
  summed over `upiFisn` per ticker in `otc_aggregate.tsv`. Surge ratio, asof **2026-09-02**.
  Distinct from the `otc` factor in `invest.tsv`, which is the model's attribution weight.

## 29. RIOT — Claude: PASS. Signal expired before it could be acted on.

Model built the case off `spot_px 17.7455`; Friday 09-04 closed **21.80**, +22.8% in four sessions
and **12.7% above** the model's own `pred_target_px_20d 19.3379`. Buying at 21.80 for a 19.34 target
is R:R **-0.37** (-11.3% up, 30.7% stop distance) with `stop_loss_px 15.1049` acting as a 31%
catastrophe floor at beta 3.86. `C_DTC 1.93` — the whole short book covers in two days, no squeeze
fuel. Only `OTC:0.0841` / OTCx 1.22 favoured it; not enough to pay 12.7% through target.

Broker screen (Merrill, 09/04 16:00 ET) agrees with the files on everything material: last 21.80,
beta 3.86 vs 3.89, short 13.24% vs 14.3% at the 08-14 settle (shorts -3.0%). Only `market_cap` is
stale in `invest.tsv` (6.99B vs 8.18B) because it is priced off the 17.75 spot. 52wk range
11.50-30.32 → 55% of range, +90% off the low.

## MAJOR data-integrity item — the prealpha run is 4 sessions stale

**Every row in `poc/20260902/mm_prealpha/invest.tsv` carries `asofdate 2026-08-31`**, 111/111,
despite the folder being named `20260902`. The folder name is not the data date.

**27 of the 111 have already traded through their 20d target** between 08-31 and the Friday 09-04
close. Their "BUY" is an expired signal, not an entry:

| Sym | spot | Fri | tgt20d | drift | past tgt |
|---|---|---|---|---|---|
| EOSE | 2.93 | 3.88 | 3.23 | +32.4% | +20.2% |
| HUT | 77.48 | 93.54 | 81.46 | +20.7% | +14.8% |
| RIOT | 17.75 | 21.80 | 19.34 | +22.8% | +12.7% |
| IREN | 37.22 | 44.68 | 39.96 | +20.0% | +11.8% |
| BE | 213.13 | 252.87 | 226.76 | +18.6% | +11.5% |
| CIFR | 14.58 | 17.74 | 15.92 | +21.7% | +11.4% |
| BTDR | 10.41 | 12.38 | 11.52 | +18.9% | +7.5% |
| ALMS | 9.38 | 11.10 | 10.38 | +18.3% | +7.0% |

Then ASTS DAVE CORZ FOUR AEHR MARA PENG GCT OPK ALGT HLF SOFI AXTI ICHR LUMN SANM IOVA HMY STRL,
all past target by less than 7%.

The crypto-miner cluster (RIOT, IREN, HUT, CIFR, BTDR, CORZ, MARA) ran together and overshot
together — treat it as one correlated block, not seven independent signals.

**Screening rule to apply before any further picks: reject any name where the Friday close is
already above `pred_target_px_20d`.** The 09-08 picks survive it — WEN drifted **-2.9%** (8.27 →
8.03) and BWXT **-2.3%** (161.28 → 157.59), i.e. both are cheaper than the model's entry assumption.

---

## Web grounding, 2026-09-08 — replaces the missing Gemini intraday grounding step

Claude has `WebSearch` / `WebFetch` in this session. Some finance domains are blocked by the
egress proxy (**finance.yahoo.com, stockanalysis.com, www.cnn.com** all returned `EGRESS_BLOCKED`);
search result summaries and non-blocked sites work. Search snippets echoed BWXT "closed at $157.59
on September 8" — that is Friday 09-04's close, the same number as `liquidty.tsv`. **Search engines
restate stale closes as if live; do not take a price from a snippet.** Prices still come from the
broker screen.

## 30. WEN — Claude REVERSES decision 22. PASS.

The pick was wrong, and grounding is what caught it. Every factor gate cleared because none of the
files carry news:

- **2026-08-27: Trian shelved the take-private.** Stock fell ~13% to $7.90 as the takeover premium
  was wiped out. Trian is the largest holder.
- **Full-year 2026 outlook withdrawn.** US same-restaurant sales **-7%**, US traffic **-12.5%**,
  global systemwide sales -6.5%, lower net income, higher costs, EPS decline.
- **Dividend cut to $0.07/qtr** to fund a five-point turnaround under new CEO Bob Wright.
- Citi reaffirmed **Hold**, PT $8.25. Next earnings **2026-11-11**.

The signal is `source=OTC_SPIKE` with `asofdate 2026-08-31` — **four days after the Trian collapse**.
The OTC notional the model fired on is almost certainly unwind and repositioning flow out of a dead
deal, not accumulation. `ConvScore 268 / A+B+C` was measuring the flow around a break. The 32.5% of
float short is a broken-turnaround short, not squeeze fuel (`C_DTC 3.9` — it covers easily).

**Generalised lesson: a high ConvScore on a name that just lost a deal premium is a sell-side
footprint. The factor files cannot tell accumulation from liquidation — only grounding can.**

## 31. BWXT — Claude: now the top pick of the residual set.

Grounding cuts the other way here. The pullback has no fundamental break behind it:

- **2026-08-26: US Army selected BWXT's BANR for the Janus program** — 5 companies, up to **$2.2B
  over 5 years**; BWXT deploys a 20MW reactor at Fort Campbell, KY (construction late 2028,
  operations early 2030s).
- **2026-09-03: selected to develop the conceptual design for an NNSA Lithium Processing Facility.**
- **Q2 2026: revenue +18%, GAAP EPS +14%**, Commercial Operations revenue +72%, operating income
  +254%, **backlog +40% y/y**, 2026 guidance raised.
- Wells Fargo upgraded to Equal Weight on valuation; Deutsche Bank kept Buy with a small PT trim.
- **Investor Day 2026-09-29.**

So the `OTC_SPIKE` at `asofdate 2026-08-31` sits five days after Janus — news-driven flow with a
real positive catalyst behind it. Opposite polarity to WEN.

Against it, stated plainly: stock is **down ~20-27% over 90 days** (momentum is against the entry);
**insiders sold $9.0M over 12 months with no purchases**; convergence in the files is thin
(ConvScore 70, **flag A only**); Investor Day on 09-29 is event risk inside the 20d horizon; and
the book **already holds $2,211**, so a further add crosses the $2,500 SMALL line.

File data that grounding confirmed rather than contradicted: market cap $14.44B (`liquidty.tsv`
and `demand_converge.tsv` agree with the web), Friday close 157.59, float 99.2%, short 3.0% of
float, `C_DTC 3.23`, `PeakT:21`, `prob 0.9698`, stop 150.09 = 10.6 vol-units below the close.

WEN's market cap also checks out ($1.50-1.57B across the three files vs $1.53B on the web) — the
files were accurate. Being accurate and being current are different things.

---

## Grounding sweep of the residual set, 2026-09-08

Pre-screen applied first (new rule from the staleness finding): **15 of the 41 remaining names were
out on the files alone** — 13 SPENT (Friday close already above `pred_target_px_20d`: AXTI BTDR
CIFR DAVE FOUR GCT HLF HMY HUT IOVA IREN PENG SANM) and 2 BROKEN STOP (BAND stop 47.34 vs close
43.77; CRDO stop 174.45 vs close 170.57). 26 stayed live and were ranked by R:R; the ones whose
R:R could actually support a trade were grounded.

## 32. WGS (GeneDx) — Claude: BUY candidate, second to BWXT.

Grounding is constructive and independently corroborates the model:
- Q2 volume and revenue **exceeded guidance**, **profitability achieved ahead of schedule**.
- Canaccord (Kyle Mikson) raised PT to **$90** from $75, Buy. The model's `pred_target_px_20d` is
  **90.29** — an independent analyst and the pipeline land on the same number.
- +32% over the past month but still **-57% YTD**; market cap $2.57B; Mark Gardner appointed
  President 06-15.

Files: `ConvScore 174.7` with flags **A+B+C** (three legs converging), OTCx 1.06, otcFac 0.490,
`C_DTC 6.39` on **33.0% of float short** — a real short base against improving fundamentals, and
it takes 6+ days to cover. Stop 77.75 = **11.5 vol-units** below the close, robust. PeakT 6,
beta 1.47, DVOL $41m, not held, no open order.

Against it: **R:R 0.52** — only +5.0% upside against a 9.6% stop. The story is better than the
geometry. That is the whole case against.

## 33. OMER — Claude: PASS on structure, not on story.

Grounding is better than expected: the **CHMP negative opinion was 2026-06-26** (stock -23% then),
so it is ten-week-old news, not the cause of the 08-31 OTC spike. Narsoplimab is **FDA-approved
since Dec 2025**, and YARTEMLEA's first full commercial quarter showed "strong momentum" (Q2
reported 08-12). PT cut to $33, still far above 18.95. RSI 12.6, oversold.

PASS anyway on trade structure: **stop 17.78 is 3.2 vol-units** below the close — the same
hair-trigger tier as SQM (3.2) and BFLY (3.3) — for **+5.6% of upside**, PeakT 4. A stop inside the
noise on a name with an EU re-examination pending is a coin flip, not an edge.

## 34. CENX — Claude: PASS. Right story, wrong entry.

Fundamentals ground well: Q2 EPS **$2.46 vs $2.30** est, **UBS initiated Buy** (Aug 2026), BMO Buy,
40% stake in a new US smelter JV with EGA, buybacks expected as capex eases H2 2026, and persistent
**50% US tariffs** on imported aluminum. But `D_RSI 98.2` — maximally extended, and one of the
sell-side pieces is literally titled "The Rally Still Has Plenty Fuel." Buying at RSI 98 for +7.6%
is chasing. Already held $1,390.

## 35. EVCM — Claude: PASS. Falling knife with insiders selling into it.

Down **~14% in a week**, trading near the **52-week low of $7.66** (~$8.07 vs $8.77 on 09-02), P/E
45.72. Director **Eric Remer sold $117,961** (14,664 shares) across 09-02 → 09-04, i.e. selling into
the decline. `ConvScore 52.3` with **no flags** and DVOL $1m. The OTC spike here reads as
distribution.

## 36. CNXC — Claude: PASS. Guidance cut.

Stock **dropped 24%** on Q2; next-quarter revenue guide 2.4% below consensus; **full-year revenue
guidance cut** $10.11B → $9.98B; **-45.6% YTD**; analyst PTs trimmed by $12 to $25. Already held
$2,425. **Unresolved discrepancy: a search snippet quotes CNXC at $22.41 while `liquidty.tsv` has
the 09-04 close at 32.16.** Verify on the broker screen before trusting either.

## 37. LPL — Claude: PASS. Miss, no catalyst.

Q2 EPS **$0.62 vs $0.69** est (revenue beat, $4.09B vs $3.85B). 52wk range 2.76-5.83, close 3.30 is
near the low end. Next earnings 10-28, outside the 20d horizon. `ConvScore 73.6`, flag D only.

## 38. QUBT — Claude: PASS. Sector beta, no company catalyst.

Only news is sector-level: the American Quantum Competitiveness Act advanced 09-05, and quantum
names fell on rising Treasury yields. Rosenblatt Buy, Cantor Hold. Beta **3.79**, R:R 0.48,
PeakT 3. `ConvScore 243` with all four flags is the strongest convergence in the set, but on a
speculative name it is measuring momentum crowding, not demand.

## 39. HPK — Claude: PASS on the files, not grounded.

`C_DTC 15.99` on **42.6% of float short** (above the 12.70 level STOK was passed at), **OTCx 0.20**
against otcFac 0.639 — the IESC/RAMP pathology of leaning on a dead leg — plus RSI 86.7, PeakT 2,
DVOL $3m, beta -0.40. Five independent fails; grounding could not rescue it.

## Remaining live-but-unground names, all PASS on R:R below 0.5

QDEL 0.51 (RSI 81) · CLVT 0.49 · MBX 0.44 · BTSG 0.35 (RSI 99.0) · NAMS 0.32 · NVCR 0.27 ·
ACHR 0.27 · SMCI 0.26 (RSI 86.3) · IBRX 0.25 (RSI 94.4, DTC 15.4) · GPRE 0.22 · GFI 0.15 ·
ACLS 0.12 · MTRN 0.09 · MUX 0.08 · DXC 0.04 · VYX 0.04 · SRPT 0.02 · IDCC 0.00.

Below R:R ~0.5 the 20d upside does not pay for the stop distance regardless of what grounding
returns, so they were not searched. Stated explicitly so the cut is auditable.

---

## Thursday cache `poc/20260903/ALPHA.run.tsv` — 29 signals, and it is FRESHER than the file we used

PM asked for the `*.run.tsv` signals on 09-08. On 09-06 the instruction had been to ignore these as
"cache of older run". **That was backwards** — the Thursday run is a day newer and far stricter than
`mm_prealpha/invest.tsv`, and it should lead, not be ignored.

| | `mm_prealpha/invest.tsv` | `20260903/ALPHA.run.tsv` |
|---|---|---|
| Data date | `asofdate 2026-08-31` (4 sessions stale) | priced **09-03**; median gap to Friday's close **1.78%** |
| Candidates screened | 111 output only | **2,111**, with the reject reason for every one |
| Passed the gate | 111 | **29 (1.4%)** |
| Schema | 37 factor columns, stops and targets | STATUS/REASON/TRADESCORE/CONFIDENCE/DECISION, **no stop or target** |

Skip funnel (Thursday): TRADESCORE_LOW 1322 · CONFIDENCE_LOW 203 · ALPHA_SIGNAL_LOW 201 ·
VOLUME_LOW 187 · **POSITION_GT_1K 143** · PASSED 29 · DECISION_NOT_BUY 25 · ILLIQUID 1.
`POSITION_GT_1K` carries the basket and the value, e.g.
`POSITION_GT_1K (BASKET=Consumer, MktValue $3,430 > $1K)` — the pipeline's own position cap is
**$1K**, not the $2,500 SMALL used in this session's screens.

`SMOOTH`, `EAR` and `DD` are empty on all 2,111 rows in this file.

### Stability problem: 93% of the passed list turns over in one day

Wednesday `20260902/ALPHA.run.tsv` passed **44** of 3,105. Thursday passed **29** of 2,111. **Only
two names appear on both: BEKE and RXRX.** 27 of Thursday's 29 were not on Wednesday's list, and 42
of Wednesday's 44 dropped off. A signal set that recycles 93% of its names overnight cannot be
treated as a conviction list; it is a daily scan. Do not read a name's presence here as persistence.

### CORRECTION — BAND and CRDO are not "broken stops", they are TRIGGERED stops

Earlier logged as a data-integrity item (stop above close). Wrong diagnosis. Both stops sat correctly
below spot when written and the stock has since traded through them:

- **BAND**: spot 50.5304 (08-31) → **47.09 (Thu)** → 43.77 (Fri). Stop **47.3373** was -6.3% below
  spot; price crossed it between Thursday and Friday (-7.1% in one session). **Held $1,098.**
- **CRDO**: spot 197.5331 → stop **174.4525** (-11.7% below spot) → Fri close 170.57. Through it.

So BAND is a **held position whose stop was breached on Friday** — an exit-side item, which is the
PM's call, not a screening artifact. Flagged, not recommended.

### Thursday's 29, ranked by TRADESCORE

Columns: MaxRet / TradeScore / Confidence from the run; Thu$ = the run's price; Fri$ and Beta and
DVOL from `liquidty.tsv`; DTC from `short_aggregate.tsv` (settle 08-14); RSI and Flags from
`demand_converge.tsv`.

BEKE 97.3 · BAND 96.8 · CADL 96.7 · GPCR 96.6 · REPL 96.5 · VYX 96.4 · HPP 96.1 · ZURA 93.7 ·
FROG 93.0 · APTV 90.8 · RYAN 90.6 · ETSY 90.4 · MNSO 89.7 · SPRY 89.7 · PCG 89.6 · HSAI 89.3 ·
HWM 88.5 · CSIQ 88.0 · RXRX 87.5 · EIX 87.2 · AON 86.1 · OABI 86.1 · ACHC 85.1 · HLF 85.0 ·
RIG 85.0 · WING 85.0 · ZS 85.0 · APLD 84.6 · NVTS 84.6

**17 of the 29 were never screened this session** — they are absent from the 111: BEKE, GPCR, HPP,
ZURA, FROG, APTV, RYAN, MNSO, SPRY, PCG, HSAI, HWM, RXRX, EIX, AON, OABI, ACHC, RIG, WING, ZS,
APLD, NVTS.

**`mm_micro` contradicts the run on 9 of them** — GPCR, APTV, PCG, HSAI, HWM, CSIQ, ACHC, APLD and
NVTS all carry `action=SELL` in `mm_micro/predict.tsv` while the Thursday run rates them STRONG_BUY.
The two models disagree; neither is authoritative on its own.

Notable: **NVTS** already has open BUY limit orders in `broker/open_orders.tsv` (IRA 2 x148,
ROTH 1 x71) and shows **+$1,071** realized — the existing order agrees with Thursday's signal.
**APLD** is the book's largest realized winner at **+$5,596** and is signalling again.
**HWM** is held $2,344 (over the $1K pipeline cap but it passed anyway — worth checking why).

No stops or targets exist in this file, so **R:R cannot be computed for the 17 new names.** Any
entry off this list needs a stop set by hand.

## Thursday 09-03 signals sorted by otc factor descending (PM doing manual DD)

**Only 7 of the 29 have an otc factor.** `otc` lives in `mm_prealpha/invest.tsv`; the other 22
Thursday names are not in that file, so they have no otcFac, no target, no stop, no R:R and no
PeakT. Those 22 are sorted by OTCx instead, below the divider. Thu$ is the run's own 09-03 price;
Fri$ is `liquidty.tsv`'s 09-04 close.

```
  # Sym    otcFac    OTCx   OTC$m  DVOL$m Sector       Thu$    Fri$   MaxRet TScore    Up%   Rsk%   R:R  PkT  Beta Micro   Held$   Real$  Status
  1 ETSY    0.5287    0.32      25     226 Consumer Cy   81.72   76.51   10.8%  90.4%   15.4    3.9  3.95   11  1.17 -           -       -  PASS
  2 BAND    0.5030    0.55      17      35 Technology    47.09   43.77   27.0%  96.8%   23.4   -8.2     -   25  2.30 -        1098       -  STOP HIT
  3 VYX     0.2133    1.05      16      21 Technology     8.98    9.14    9.0%  96.4%    0.4    9.0  0.04   30  1.24 -           -       -  PASS
  4 CSIQ    0.0000       -       0      25 Technology    13.53   13.22   11.2%  88.0%    3.0   10.5  0.28   11  2.68 SELL        -    -152  -
  5 HLF     0.0000       -       0      18 Consumer De   12.17   12.38   17.6%  85.0%   -2.0   13.0 -0.15   14  1.24 -           -       -  SPENT
  6 CADL   -0.0017    0.73       1      15 Healthcare    12.97   12.78   14.0%  96.7%    6.6    9.0  0.74   14  2.03 BUY         -       -  -
  7 REPL   -0.7150    1.16      33      46 Healthcare    15.29   15.04   58.8%  96.5%   33.8   40.8  0.83    4  1.21 BUY         -       -  -
--- no otc factor (not in invest.tsv); sorted by OTCx ---
  8 RYAN         -    1.47      49      52 Financial S   42.34   41.91   10.2%  90.6%      -      -     -    - -0.24 -           -       -  NEW
  9 BEKE         -    1.16      55      76 Real Estate   17.91   17.92    8.5%  97.3%      -      -     -    -  0.83 -           -       -  NEW
 10 APLD         -    1.01      54     422 Technology    25.91   26.37    8.9%  84.6%      -      -     -    -  3.95 SELL        -   +5596  NEW
 11 HSAI         -    0.88      12      32 Consumer Cy   18.46   18.89   12.7%  89.3%      -      -     -    -  2.93 SELL        -       -  NEW
 12 PCG          -    0.80      52     686 Utilities     13.96   14.30   20.8%  89.6%      -      -     -    -  0.19 SELL        -       -  NEW
 13 MNSO         -    0.78      15      11 Consumer Cy    9.67    9.56   11.9%  89.7%      -      -     -    -  0.95 -           -       -  NEW
 14 HWM          -    0.75      85     662 Industrials  260.49  259.27    9.5%  88.5%      -      -     -    -  1.08 SELL     2344       -  NEW
 15 WING         -    0.74      20     126 Consumer Cy  113.15  109.21    9.8%  85.0%      -      -     -    -  1.01 -           -       -  NEW
 16 ACHC         -    0.70      15      36 Healthcare    28.38   28.13    8.1%  85.1%      -      -     -    -  0.94 SELL        -       -  NEW
 17 OABI         -    0.70       0      11 Healthcare     5.04    4.33    9.9%  86.1%      -      -     -    -  1.44 BUY         -       -  NEW
 18 SPRY         -    0.62       3      10 Healthcare     5.67    5.62   20.3%  89.7%      -      -     -    -  1.65 -           -       -  NEW
 19 EIX          -    0.59      52     371 Utilities     55.19   56.77   30.5%  87.2%      -      -     -    -  0.08 -           -       -  NEW
 20 ZS           -    0.50      35     512 Technology   172.73  169.80   21.9%  85.0%      -      -     -    -  1.09 -           -       -  NEW
 21 HPP          -    0.48       2       7 Real Estate   12.74   12.61   10.2%  96.1%      -      -     -    -  1.26 -           -       -  NEW
 22 RXRX         -    0.44       9      52 Healthcare     3.44    3.63    9.3%  87.5%      -      -     -    -  2.97 -           -       -  NEW
 23 NVTS         -    0.39       4     158 Technology    11.21   11.80    8.9%  84.6%      -      -     -    -  4.70 SELL        -   +1071  NEW
 24 GPCR         -    0.30      24      31 Healthcare    47.34   47.34    8.7%  96.6%      -      -     -    -  0.86 SELL        -       -  NEW
 25 AON          -       -       0     283 Financial S  327.00  323.09   11.7%  86.1%      -      -     -    - -0.20 -           -       -  NEW
 26 APTV         -       -       0     201 Consumer Cy   46.53   47.95   11.2%  90.8%      -      -     -    -  1.22 SELL        -       -  NEW
 27 FROG         -       -       0     182 Technology    90.61   87.60   21.6%  93.0%      -      -     -    -  1.49 -           -       -  NEW
 28 RIG          -       -       0     239 Energy         6.02    5.85   10.6%  85.0%      -      -     -    -  0.68 -           -       -  NEW
 29 ZURA         -       -       0       9 Healthcare     5.67    6.23    8.8%  93.7%      -      -     -    -  1.85 -           -       -  NEW
```

**The two models disagree at the top.** REPL scores TradeScore 96.5% / MaxRet 58.8% on Thursday but
carries `otc = -0.7150` in the prealpha file — the most negative otc factor of any Thursday name.
CADL is 96.7% with `otc = -0.0017`. Both would have been cut by this session's "filter out negative
otc" screen, and both are `micro:BUY`. Five Thursday names (AON, APTV, FROG, RIG, ZURA) have no row
in `otc_aggregate.tsv` at all, so their blank OTCx is unmeasured, not zero.

PM is doing manual DD from here.

---

# 2026-09-12 — full book reconciliation and new-name screen

## Capital deployed 09-04 -> 09-11 (Merrill, the six accounts in the PM's export)

**Net new cost basis $42,593.06** — not the ~$35.2K the 9/5 scratch pad projected, because Batch A
filled as well.

| | |
|---|---|
| 16 brand-new names | +$28,126.09 |
| 20 adds to existing | +$21,097.90 |
| 1 exit — ARGX (cost) | -$5,160.00 |
| 3 trims (OXY -$1,467.03) | -$1,469.13 |
| **net** | **$42,593.06** |

Cost basis 09-04 $495,589.29 -> 09-11 $538,182.35 (export implies $538,183.66; $1.31 rounding).
New names: NVTS $4,319 · PCG $2,077 · APLD $2,042 · KEP $1,834 · RYAN $1,753 · FMX $1,740 ·
RTO $1,693 · TXN $1,535 · BFLY $1,534 · PINS $1,500 · RYTM $1,498 · LEGN $1,452 · EIX $1,395 ·
CIFR $1,350 · RCAT $1,222 · OMCL $1,181.

## Book state at 09-11

241 positions · equity $534,643.12 · unrealized -$3,540.54 (-0.66%) · 97 winners / 144 losers ·
median position $1,982 · top-10 = 15.0% of equity · cash -$8,524.39 · total $1,099,132.35.

**58 positions exceed the $2,500 SMALL cap and are 43.5% of equity.** Nine exceed $5,000.
**OXY alone is $27,929.03 = 5.22%** (11x SMALL); with OXYWS (+697.98%) the complex is $30,141 = 5.64%.

## Scorecard on this session's calls

| Name | Result | Note |
|---|---|---|
| BFLY | +0.34% | filled |
| PINS | -4.75% | filled |
| IESC | **never filled** | limit not reached |
| BWXT (Claude #1) | **-3.57%** | 150.12 vs 157.59 = -4.7% off 09-04 |
| WGS (Claude #2) | not bought | |
| BAND | **+22.54%** | 56.87 vs 43.77 = **+29.9%** in five sessions |
| HWM | **-9.90%** | GTC filled at 254, then fell to 229.61; now $2,984.93, over cap |

**Claude was wrong on BAND and the PM's own note was right.** Claude reported the stop as breached
on 09-04 at 43.77 (factually true); the 9/4 scratch pad said "hold the accumulation, do not cut."
The stop-breach framing was accurate and useless. Lesson: a breached stop on an accumulation the PM
has explicitly marked do-not-cut is an observation, not a finding.

Passes that held, none bought: CNXC -13.97% (28.24 — the $22.41 search snippet was wrong, the
file's 32.16 was right for 09-04) · SQM -13.89% · SPT -6.98% · CENX -5.8% off 09-04 ·
RIOT/WEN/EVCM/OMER/QDEL/AEHR/IT/INBX/RAMP/FDX all NOT HELD.

## New-name screen — 193 signal names the PM does not own, 66 with 2+ source corroboration

Cuts applied: micro=SELL · already decided this session · SPENT (close above target) · negative R:R ·
C_DTC above the 12.7 level STOK was passed at · beta>3 spec (the class the PM dropped on 9/5).

### 40. SAIC — Claude: the standout new name.

Grounding is unambiguously positive:
- Q2 EPS **$3.01 vs $2.31** consensus; revenue **$1.880B vs $1.766B**.
- **FY27 guidance raised**: adj EPS to $10.65-10.75 from $9.90-10.10; revenue to $7.2-7.3B from
  $7.0-7.2B.
- PT raises: UBS $108 -> $123 (Neutral), Truist $110 -> $130 (Hold). Dividend $0.37, ex 10-09.
- One caveat in the coverage: "higher guidance meets soft bookings."

Files: **beta 0.31** · DVOL $62m · `C_DTC 7.2`, short 6.8% of float · ConvScore 118, flag A ·
RSI 75 (extended) · prealpha + runWed, 09-02 decision PASS.

Why it fits: government IT / defense services is uncorrelated with both the semis complex that drove
this week's gains and the biotech that drove the losses. The book's problem is not idea supply, it is
that 43.5% of equity sits above cap in correlated sleeves.

### 41. BEKE — Claude: second, with a named country risk.

- Q2 EPS **$0.42 vs $0.28** (+50% beat). 2026 Interim Report and cross-market buyback disclosure
  both filed **09-08**.
- +9.90% 1-month, +14.07% YTD at $18.32. SWS DCF fair value **$24.93** vs $18.32.
- **The only name appearing on BOTH ALPHA.run days**, and Thursday's highest TradeScore at 97.3%.

Files: beta 0.83 · DVOL $76m · short **3.9% of float**, `C_DTC 10.3` · ConvScore 52, no flags ·
RSI 38. Against it: China residential property platform — a single policy decision moves it, and
convergence is thin.

### 42. AON — Claude: watch, not buy. Lowest beta available but no convergence.

`beta -0.20` and short **1.6% of float / DTC 3.6** — the cleanest short profile of all 66. Consensus
Moderate Buy, PT $399.12 vs $323.09. Q2 EPS $3.81, revenue +2.2%.

Against: the **$17B USI Insurance acquisition** is not EPS-accretive until **2028**, with stated
investor concern on leverage and execution; CEO Greg Case acknowledges a **flat near-term P&C
market**. ConvScore 49 with no flags — nothing is converging. A 2028 payoff is outside a 20-day
horizon.

### 43. QDEL — Claude: PASS, against the PM's own note.

The 9/4 scratch pad ranks QDEL the **closest** velocity-turn candidate, and three pipeline models
(inv111 + meanrev + prealpha) corroborate it — the strongest cross-model agreement in the set.
Grounding still says no:
- Q2 revenue +2% overall but **China -23%** and a softer respiratory market.
- **Full-year guidance revised down and free cash flow guidance WITHDRAWN.**
- 3 analysts average **Hold** with a 12-month PT of **$12.00** — *below* the 13.97 close.

Withdrawn FCF guidance is the same pattern that killed WEN. Flow can be real while the business is
impaired; the flow models cannot see a withdrawn guide.

### 44. WING — Claude: PASS. Comps down five straight quarters.

Same-store sales **-7.5% in Q2 2026**, the fifth consecutive decline, and the updated 2026 outlook
guides domestic SSS to **-4% to -6%**. Upgraded sell->hold only after a >50% price fall; fair value
trimmed to ~$286 from ~$305. It also already moved: **+6.0% on 09-11 to $117.10** vs 109.21 on 09-04,
so the RSI 13 oversold setup the files showed is spent.

### 45. MNSO — Claude: PASS. Loss-making and a flagged capital-allocation problem.

Q2 2026 **net loss CN¥289.2M**, LPS CN¥0.96 against a CN¥1.60 profit a year earlier, on revenue
+17%. Downgraded to **HOLD from BUY** on "questionable capital allocation and execution risks", PT
cut ~$19.30 -> $14.32 (one house $26 -> $16). The Yonghui Supermarket stake is cited as
misallocation.

## Note: no stops exist for any of the three candidates

SAIC, BEKE and AON are absent from `mm_prealpha/invest.tsv`, so there is no target, no
`stop_loss_px`, no R:R and no PeakT for any of them. A stop has to be set by hand.

---

# 2026-09-12 — gain-protection framework

Long design thread with the PM. Recorded because several conclusions reversed my own earlier
positions, and two of my framings were simply wrong.

## Where I was wrong

1. **"The floor and the buffer collide."** I claimed a 15% locked floor and a 15% buffer were
   simultaneously satisfiable only above +35.3%. Wrong premise: in the PM's method the floor is an
   **output** of (price, cost, buffer), not an input. There is no collision.
2. **"OXY is an 11x sizing breach."** OXY/OXYWS are a **hedge**, not trades. I repeated
   "58 positions / 43.5% of equity over cap" several times with OXY at the top. Correct figure is
   **57 / 40.5% of the trading book**, and the hedge is not size-governed at all. Trading-book
   beta ex-hedge is **1.54**, not 1.43; the hedge contributes **+$11,072** against the trading
   book's **-$14,611**.
3. **BAND.** I reported the stop as breached on 09-04 at 43.77 (true) and read it as a finding.
   The PM's 9/4 note said "hold the accumulation, do not cut." It is 56.87 — **+29.9% in five
   sessions.** Accurate and useless.

## Realized-lot findings (recomputed — the file's own pct column is broken)

`RealizedPnlPct` is unusable: SMH shows +1.5% on $13,200 of profit. Recomputed from
`RealizedPnl / AcquisitionCost` across 1,107 lots, 714 winners (64%):

| | |
|---|---|
| winner median | +15.3% |
| p75 / p90 / p95 | +37.0% / +82.4% / +128.7% |
| max | +315.8% |
| loser median / p10 / worst | -10.2% / -33.5% / -77.3% |

**78.9% of all realized profit came from lots past +30%; 45.8% from past +100%.** The +20-30%
band produced **6.9%**. A hard 20-30% profit-target rule would have truncated four-fifths of the
book's profit — so option (a) is refuted by the PM's own history. Winner median holding period
**61 days**, loser median **60 days** — holding period currently carries zero information.

## Volatility, not beta, sets the buffer

Same-beta pairs from `liquidty.tsv`: WVE (β1.30, vol 1.68%) vs WWD (β1.27, vol 0.38%) —
**4.4x different daily range at the same beta**. A flat 10% buffer spans 6.5 to 28.4 sigma-days
across the book. Fixing `k` fixes the stop-out *probability*; the percentage then varies.

## The gain constraint — the one structural result

```
hi = G/(1+G)    =>    stop = P(1 - G/(1+G)) = C(1+G)/(1+G) = C exactly
```

Capping the buffer at `G/(1+G)` **guarantees the stop never sits below cost.** Structural, not a
post-hoc check. Resolves the 68-name / $140,181 group that had positive P&L but implied stops
below cost.

## Cluster risk — why naive per-name stops are dangerous here

On a single -5% index day, beta-scaled, **$64,176 = 12.7% of the trading book** would stop out
simultaneously. Per-name stops are individually sound and collectively correlated. Hence the
8%-of-equity cluster cap and the FOMC/CPI blackout in the spec.

## Sizing argument — PM is right

$2,500 = **50bps of trading-book equity** (23bps of the $1.1m total). Worst single realized lot
in history -77.3%, so max single-name damage is **0.38% of equity**; to zero, 0.50%. Manual
discretion at that size is lower-risk than automated stops, which would add the clustering
failure above. But two caveats: the **sleeve** does not diversify (47 semis/AI names x 50bps =
19.7% of equity at beta ~3; a -5% day costs 3.0% of equity = **8x** the worst single-name
outcome), and ten positions run 96-136bps, 2-2.7x SMALL.

## >100-day loser rule — discretionary drift check, not a gate (PM correction)

Five names today: CAT -9.43%/121d, CTOS -9.24%/120d, GFI -7.49%/144d, GOOGL -5.30%/113d,
NVO -3.86%/113d. $7,179 = 1.4% of equity, nothing worse than -9.5%. Well calibrated. Note the
real damage (RARE -47%, PL -31%, STM -27%, WVE -23%) is all **under** 100 days and has not
triggered it yet.

## Alpha-modulated buffer — tested, null result

Modulating the vol-scaled buffer by RSI/VEL/PeakT does **not** rescue the negative-floor group:
27 names clear a positive floor vol-only, 27 modulated. Two rescued (NRGV, VST), two lost.
Widening washed names pushes them further negative. **But** it correctly surfaced ten
washed-and-turning names (DAC, VALE, ENTG, ALT, PFE, TM, PUMP, MTSI, CEG, MRP) — early in their
move, nothing to protect yet. So the alpha state decides **whether the stop question applies**,
not the buffer size. Three regimes: ALPHA_AHEAD (no stop), ALPHA_WORKING (buffer + ratchet),
ALPHA_SPENT (tighten/harvest).

## k, and why it is banded and manual

`k` = how many of the name's own typical days the stop tolerates. `buffer% = k x SIGMA20`.
**Provenance: the PM's stated 15% on high-beta implies k ~ 10-14** (AXTI 9.8, POET 10.5,
NVTS 11.9, QBTS 12.9, BE 13.0, ASTS 13.5, APLD 14.3). Not fitted to anything.

PM decision: **`k` is a per-name band from {8,10,12,15,20}, chosen manually, set once.** Reasons
it beats a continuous formula here — legibility, order stability, discretion sits where the PM
said it belongs, and auditability (you can later separate PM judgment from model drift).

The honest tension the band resolves: **`k` is noise tolerance, `k x sigma` is give-back
tolerance, and on a high-sigma name the two conflict.** DAC at k=20 gives 4.6% give-back; BE at
k=20 gives 23.0%. No formula settles that.

**AXTI is the instructive limit:** G=12.66%, sigma=1.53 — even k=8 gives 12.3% while the gain
allows only 11.2%. **No band protects it.** Correct output is no order.

**Rollout recommendation:** start with the nine sigma<0.40 names (DAC ITUB DE VALE PBR KBR HAFN
DHT TRMD) where the gain constraint never binds and no band judgment is needed. The semis/AI
sleeve is where protection is most wanted and the method weakest.

## Broker mechanics — PM correction accepted

PM observes Merrill's `TrailingStopLimit` does not ratchet: it fixes stop and limit $ off spot at
placement. General documentation describes a ratcheting **Trailing Stop** — a different order
type, which Merrill's own list does not even enumerate alongside TrailingStopLimit. Unresolved;
one call to Merrill settles it. **The spec does not depend on it** — every order is a plain
stop-limit at an explicit price, re-issued on AMEND.

Four live orders were placed and not adjusted (PM out of office): PBR 7% (+19.98%), DAC 5%
(+15.21%), ITUB 7% (+13.55%), ALT 5% (+11.22%) — all protecting entry, not gain, if static.
ARGX's order is resolved: **by design**, 7% stop on a >90-day lot at +25% to force the rotation.

## Deliverable

`spec/spec_gain_protect_buffer_rev2.md`, also on Drive at `quantbot/tablet/` as
`spec_gain_protect_buffer_rev2.md` (id `1N5o-GQ9qVuB3ebRGcu9dgB7mXEKqpnTO`, 26,058 B).
Rev 1 renamed `spec_gain_protect_buffer_rev1_SUPERSEDED.md`.

Rev 2 adds: banded manual `k` with a set-once lifecycle (§2.7, §7.1), a normative `SIGMA20`
calculation (§3A — log returns, 20 sessions, Bessel-corrected, non-zero mean, winsorised at
5x SIGMA60, 5-day median smoothing, regime-shift flag), and the sigma-asymmetry proof (§3A.8:
because the ratchet takes `max(prior, raw)`, a vol spike cannot loosen an existing stop — sigma
drift can only tighten). Nine open decisions in §15.

**Nothing in this thread is an order or a recommendation to trade.** Levels, sizes and every exit
remain the PM's.
