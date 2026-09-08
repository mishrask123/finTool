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
