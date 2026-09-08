# PM decision log — 2026-09-07 (Labor Day, market closed)

Decisions recorded the turn they were made ([[reference-worksheet-set]]).
`worksheet_set.cmd` cannot run remotely — fold this into the worksheet at the PC.
Source universe: `poc/20260902/mm_prealpha/invest.tsv` (asof Mon 08-31, 111 names).

## PM DECISIONS

| Date | Symbol | Decision | Note |
|---|---|---|---|
| 2026-09-07 | ETSY | **PASS** | PM call. Was the best-supported name in the filtered cut (R:R 4.0, DVOL $226M, beta 1.17, grounded 09-04). Passed anyway. |
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

## Standing data-integrity items

- **BAND / CRDO / ASAN** — `stop_loss_px` above Friday's close; fire instantly if placed as written.
- **BFLY** — same class of problem, not yet inverted: 4.2% stop at beta 3.41.
- `pnl/20260904.tsv` is a **14:32 ET intraday snapshot**, not the close; its PnL understates.
- `limit_px` is the 20d TARGET, not an entry limit (identical to `pred_target_px_20d`, 111/111).
