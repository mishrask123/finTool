# PreAlpha `invest.tsv` — all 111 symbols, re-read 2026-09-07

Source: `poc/20260902/mm_prealpha/invest.tsv`, asofdate **2026-08-31 (Mon)**, 111 rows,
all `direction=BUY`. Prices re-struck against `input/eod_price.tsv` = **Fri 09-04 close**.
Cross-checked against `mm_micro/predict.tsv` (asof Wed 09-02) and the 44-name Gemini cache.

---

## ⛔ THREE CORRECTIONS to how this file was read in the first Tuesday card

**1. `limit_px` is NOT an entry limit — it is the price target.**
`limit_px == pred_target_px_20d` on **111/111 rows**, and sits **above spot on 111/111**
(zero rows below). There is **no entry price anywhere in this file**. The old card's
"close still at/below limit = live entry, −25%" actually meant "25% of predicted upside
remains". The `Upside` column below is the corrected reading.

**2. The liquidity leg is dead.** `liquidity` = `0.0` on all 111 rows, and every
liquidity-derived attribution — `liq`, `cross_otc_x_liq`, `cross_trend_x_liq` — is
exactly zero. Per the risk suite, *liquidity is THE driver of PnL* in this book. The
model is blind to it. Looks like a wiring bug in the prealpha writer, worth chasing at
the PC.

**3. ⭐ `PeakT` is measured from 08-31, and its median is 7 days — not 20.**
Tue 09-08 is **8 calendar / 5 trading days** after the asofdate. So by Tuesday's open:

| Reading | Peak already passed |
|---|---|
| calendar (PeakT ≤ 8) | **62 / 111 (56%)** |
| trading days (PeakT ≤ 5) | **38 / 111 (34%)** |

⚠️ UNVERIFIED whether PeakT counts calendar or trading days — the file does not say.
Either way, **the majority of this list is past or at its predicted peak before you can
trade it.** This is the single most important fact on the page for a 2-week absence.

**Also:** `dd`="HIGH: Extreme Gap Risk", `smooth`="NOISY: Erratic Move" and
`direction`="BUY" are constant on all 111 — zero information. `r2 ≥ 0.999` on 91/111
(in-sample fit, not forecast skill). `prob` correlates with nothing (max |r| = 0.116
against any candidate driver), so **do not rank by prob** — the old card did.
Dominant factor: `otc` on 61/111, `other` 32, `price` 10, `short` 8 — this is an
OTC-flow signal.

---

## A. BROKEN STOPS — 3 names, do not place as written

`stop_loss_px` is at or above Friday's close; placed as-is these fire instantly.

| Sym | Sector | Spot 08-31 | Fri 09-04 | Move | Target | Upside | Stop | StopDist | PeakT | Factor | Micro | Grounded |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| BAND | Technology | 50.53 | 43.77 | -13.4% | 54.03 | +23.4% | 47.34 | +8.2% | 25d | other |  | 09-04 |
| CRDO | Technology | 197.53 | 170.57 | -13.6% | 211.65 | +24.1% | 174.45 | +2.3% | 24d | price |  |  |
| ASAN | Technology | 9.82 | 8.81 | -10.3% | 10.32 | +17.2% | 8.94 | +1.4% | 5d | short |  |  |

---

## B. TARGET ALREADY EXCEEDED — 27 names, predicted move is spent

Friday's close is at or above the model's own target. Not "you missed the entry" —
the forecast has been met. Note the crypto-miner / power cluster (RIOT CIFR HUT IREN
BTDR CORZ MARA) moving together: basket beta, not 7 independent edges.

| Sym | Sector | Spot 08-31 | Fri 09-04 | Move | Target | Upside | Stop | StopDist | PeakT | Factor | Micro | Grounded |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| EOSE | Industrials | 2.93 | 3.88 | +32.4% | 3.23 | -16.8% | 2.49 | -35.9% | 6d | price |  |  |
| RIOT | Financial Services | 17.75 | 21.80 | +22.8% | 19.34 | -11.3% | 15.10 | -30.7% | 6d | other |  |  |
| CIFR | Technology | 14.58 | 17.74 | +21.7% | 15.92 | -10.3% | 12.56 | -29.2% | 2d | otc |  |  |
| HUT | Financial Services | 77.48 | 93.54 | +20.7% | 81.46 | -12.9% | 69.32 | -25.9% | 5d | other |  |  |
| IREN | Financial Services | 37.22 | 44.68 | +20.0% | 39.96 | -10.6% | 31.56 | -29.4% | 16d | price |  |  |
| BTDR | Technology | 10.41 | 12.38 | +18.9% | 11.52 | -7.0% | 8.73 | -29.5% | 25d | other |  |  |
| BE | Industrials | 213.13 | 252.87 | +18.6% | 226.76 | -10.3% | 181.86 | -28.1% | 2d | otc |  |  |
| ALMS | Healthcare | 9.38 | 11.10 | +18.3% | 10.38 | -6.5% | 8.51 | -23.3% | 2d | otc | SELL |  |
| ASTS | Technology | 55.04 | 62.31 | +13.2% | 58.50 | -6.1% | 47.84 | -23.2% | 6d | otc |  |  |
| DAVE | Technology | 337.84 | 380.69 | +12.7% | 359.82 | -5.5% | 309.98 | -18.6% | 6d | otc |  |  |
| AEHR | Technology | 76.57 | 86.26 | +12.7% | 82.79 | -4.0% | 64.96 | -24.7% | 4d | otc | SELL |  |
| FOUR | Technology | 40.91 | 45.93 | +12.3% | 43.47 | -5.4% | 37.86 | -17.6% | 6d | other |  |  |
| OPK | Healthcare | 1.46 | 1.64 | +12.2% | 1.59 | -3.0% | 1.28 | -21.8% | 30d | otc |  |  |
| CORZ | Technology | 16.03 | 17.89 | +11.6% | 16.92 | -5.4% | 14.32 | -19.9% | 2d | otc | SELL |  |
| MARA | Financial Services | 10.22 | 11.31 | +10.7% | 10.90 | -3.6% | 7.84 | -30.7% | 2d | other | BUY |  |
| AXTI | Technology | 56.04 | 61.64 | +10.0% | 60.69 | -1.5% | 48.13 | -21.9% | 2d | otc |  |  |
| PENG | Technology | 47.19 | 51.76 | +9.7% | 50.02 | -3.4% | 42.87 | -17.2% | 10d | otc |  |  |
| GCT | Technology | 47.59 | 51.75 | +8.7% | 50.14 | -3.1% | 44.16 | -14.7% | 26d | short |  |  |
| ICHR | Technology | 52.04 | 56.38 | +8.3% | 55.64 | -1.3% | 46.65 | -17.2% | 7d | other | SELL |  |
| ALGT | Industrials | 72.30 | 78.16 | +8.1% | 75.99 | -2.8% | 65.38 | -16.4% | 27d | otc |  |  |
| HLF | Consumer Defensive | 11.50 | 12.38 | +7.7% | 12.13 | -2.0% | 10.77 | -13.0% | 14d | price |  | 09-04 |
| SOFI | Financial Services | 17.02 | 18.22 | +7.1% | 17.94 | -1.6% | 15.52 | -14.8% | 4d | other |  |  |
| STRL | Industrials | 455.64 | 486.49 | +6.8% | 486.04 | -0.1% | 407.31 | -16.3% | 4d | other |  |  |
| LUMN | Communication Serv | 6.35 | 6.77 | +6.5% | 6.71 | -0.8% | 5.68 | -16.1% | 10d | short |  |  |
| IOVA | Healthcare | 8.27 | 8.79 | +6.2% | 8.77 | -0.2% | 7.06 | -19.7% | 19d | otc | BUY | 09-03 |
| SANM | Technology | 187.22 | 198.47 | +6.0% | 197.63 | -0.4% | 173.73 | -12.5% | 22d | otc |  |  |
| HMY | Basic Materials | 19.22 | 20.27 | +5.5% | 20.23 | -0.2% | 18.02 | -11.1% | 2d | otc |  |  |

---

## C. UPSIDE REMAINS **BUT PEAK WINDOW PASSED** — 44 names (PeakT ≤ 8d)

The model still shows upside to target, but its own predicted peak date is behind us.
Per the rotation doctrine, alpha decays — these are the "too late" bucket unless the
tape says the move is still building.

| Sym | Sector | Spot 08-31 | Fri 09-04 | Move | Target | Upside | Stop | StopDist | PeakT | Factor | Micro | Grounded |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| REPL | Healthcare | 15.67 | 15.04 | -4.0% | 20.12 | +33.8% | 8.90 | -40.8% | 4d | other | BUY | 09-04 StrongEntry/INTACT |
| IESC | Industrials | 300.70 | 322.57 | +7.3% | 395.21 | +22.5% | 221.47 | -31.3% | 2d | otc |  |  |
| FDX | Industrials | 324.65 | 322.52 | -0.7% | 358.52 | +11.2% | 289.49 | -10.2% | 6d | otc |  |  |
| SQM | Basic Materials | 80.49 | 76.43 | -5.0% | 84.64 | +10.7% | 75.25 | -1.5% | 2d | otc | BUY |  |
| PINS | Communication Serv | 21.25 | 20.40 | -4.0% | 22.59 | +10.7% | 19.10 | -6.4% | 5d | otc |  |  |
| INBX | Healthcare | 124.62 | 121.17 | -2.8% | 133.31 | +10.0% | 111.91 | -7.6% | 8d | otc |  |  |
| DOW | Basic Materials | 30.44 | 29.44 | -3.3% | 32.15 | +9.2% | 27.80 | -5.6% | 5d | otc |  |  |
| EVCM | Technology | 8.07 | 7.92 | -1.8% | 8.62 | +8.8% | 7.37 | -6.9% | 7d | otc |  |  |
| WEN | Consumer Cyclical | 8.27 | 8.03 | -2.9% | 8.69 | +8.3% | 7.73 | -3.7% | 7d | other | BUY |  |
| RCAT | Industrials | 8.25 | 8.37 | +1.4% | 9.05 | +8.1% | 6.70 | -20.0% | 8d | other | SELL |  |
| IT | Technology | 189.82 | 186.42 | -1.8% | 200.99 | +7.8% | 172.34 | -7.6% | 3d | other |  |  |
| CENX | Basic Materials | 46.76 | 46.78 | +0.0% | 50.32 | +7.6% | 41.79 | -10.7% | 6d | otc |  |  |
| SOUN | Technology | 6.85 | 6.74 | -1.5% | 7.24 | +7.5% | 5.97 | -11.4% | 3d | otc |  |  |
| QBTS | Technology | 16.53 | 16.58 | +0.3% | 17.78 | +7.3% | 13.47 | -18.7% | 6d | other | SELL |  |
| QUBT | Technology | 7.90 | 8.01 | +1.4% | 8.56 | +6.9% | 6.87 | -14.3% | 3d | other |  |  |
| SMCI | Technology | 36.66 | 39.59 | +8.0% | 42.31 | +6.9% | 29.26 | -26.1% | 7d | other | BUY |  |
| CNXC | Technology | 32.27 | 32.16 | -0.3% | 34.37 | +6.9% | 29.53 | -8.2% | 8d | otc | BUY |  |
| AMPX | Industrials | 9.46 | 9.89 | +4.5% | 10.51 | +6.3% | 8.10 | -18.1% | 2d | otc | SELL | 09-03 |
| IE | Basic Materials | 10.03 | 9.99 | -0.4% | 10.61 | +6.2% | 8.95 | -10.4% | 2d | otc |  |  |
| HPK | Energy | 8.11 | 8.05 | -0.7% | 8.55 | +6.2% | 7.42 | -7.8% | 2d | otc |  |  |
| RGTI | Technology | 14.99 | 15.20 | +1.4% | 16.06 | +5.7% | 12.32 | -19.0% | 3d | other | SELL |  |
| OMER | Healthcare | 18.72 | 18.95 | +1.3% | 20.01 | +5.6% | 17.78 | -6.1% | 4d | other | BUY |  |
| MBX | Healthcare | 60.87 | 61.72 | +1.4% | 65.04 | +5.4% | 54.15 | -12.3% | 2d | otc |  |  |
| QDEL | Healthcare | 13.75 | 13.97 | +1.6% | 14.71 | +5.3% | 12.53 | -10.3% | 6d | otc |  |  |
| EYE | Consumer Cyclical | 16.69 | 16.74 | +0.3% | 17.58 | +5.0% | 15.60 | -6.8% | 2d | otc | SELL |  |
| WGS | Healthcare | 84.70 | 85.99 | +1.5% | 90.25 | +5.0% | 77.75 | -9.6% | 6d | otc |  |  |
| BTSG | Healthcare | 59.12 | 60.73 | +2.7% | 63.57 | +4.7% | 52.59 | -13.4% | 6d | short |  |  |
| SEDG | Technology | 32.41 | 34.20 | +5.5% | 35.65 | +4.2% | 27.85 | -18.6% | 6d | other |  | 09-03 |
| SONO | Technology | 15.09 | 15.36 | +1.8% | 16.00 | +4.2% | 13.78 | -10.3% | 2d | short |  |  |
| PRIM | Industrials | 72.10 | 74.43 | +3.2% | 77.51 | +4.1% | 62.77 | -15.7% | 6d | other | SELL |  |
| GPRE | Basic Materials | 14.73 | 15.45 | +4.9% | 15.98 | +3.4% | 13.02 | -15.7% | 2d | otc |  |  |
| NAMS | Healthcare | 24.95 | 25.40 | +1.8% | 26.25 | +3.4% | 22.71 | -10.6% | 8d | price |  |  |
| ACHR | Industrials | 5.57 | 5.72 | +2.7% | 5.90 | +3.1% | 5.06 | -11.6% | 4d | other |  | 09-03 |
| IBRX | Healthcare | 7.87 | 8.08 | +2.7% | 8.32 | +3.0% | 7.12 | -11.9% | 6d | other |  |  |
| IONQ | Technology | 37.76 | 39.52 | +4.7% | 40.61 | +2.8% | 32.45 | -17.9% | 4d | otc | SELL |  |
| GFI | Basic Materials | 44.64 | 47.40 | +6.2% | 48.46 | +2.2% | 40.23 | -15.1% | 2d | otc |  |  |
| ACLS | Technology | 110.43 | 115.08 | +4.2% | 116.79 | +1.5% | 100.64 | -12.5% | 5d | otc |  |  |
| RUN | Technology | 8.33 | 8.89 | +6.7% | 9.01 | +1.3% | 7.20 | -19.0% | 4d | otc | SELL |  |
| BRKR | Healthcare | 55.88 | 58.50 | +4.7% | 59.23 | +1.2% | 50.33 | -14.0% | 5d | otc |  |  |
| MTRN | Basic Materials | 234.19 | 244.24 | +4.3% | 246.83 | +1.1% | 214.04 | -12.4% | 6d | otc |  |  |
| MUX | Basic Materials | 19.10 | 20.07 | +5.1% | 20.28 | +1.0% | 17.52 | -12.7% | 4d | otc |  |  |
| DXC | Technology | 11.14 | 11.66 | +4.7% | 11.71 | +0.4% | 10.52 | -9.8% | 6d | otc |  |  |
| SRPT | Healthcare | 21.16 | 22.50 | +6.4% | 22.58 | +0.3% | 18.66 | -17.1% | 2d | other | BUY |  |
| IDCC | Technology | 319.69 | 337.94 | +5.7% | 337.96 | +0.0% | 299.29 | -11.4% | 2d | otc |  |  |

---

## D. UPSIDE REMAINS AND PEAK STILL AHEAD — 37 names (PeakT > 8d)

The only subset where the model's own timing is not already expired. **This — not the
68-name list on the first card — is the defensible short list.**

| Sym | Sector | Spot 08-31 | Fri 09-04 | Move | Target | Upside | Stop | StopDist | PeakT | Factor | Micro | Grounded |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| BFLY | Healthcare | 8.13 | 7.36 | -9.5% | 8.94 | +21.5% | 7.05 | -4.2% | 28d | otc |  |  |
| ETSY | Consumer Cyclical | 81.73 | 76.51 | -6.4% | 88.29 | +15.4% | 73.53 | -3.9% | 11d | otc |  | 09-04 |
| TNDM | Healthcare | 21.25 | 19.90 | -6.3% | 22.63 | +13.7% | 18.82 | -5.4% | 28d | otc |  |  |
| FLNC | Utilities | 10.45 | 10.35 | -0.9% | 11.75 | +13.6% | 9.02 | -12.8% | 14d | otc | SELL |  |
| QURE | Healthcare | 47.41 | 44.50 | -6.1% | 49.98 | +12.3% | 36.40 | -18.2% | 16d | other |  |  |
| BWXT | Industrials | 161.28 | 157.59 | -2.3% | 171.70 | +9.0% | 150.09 | -4.8% | 21d | otc |  |  |
| STOK | Healthcare | 30.88 | 29.81 | -3.5% | 32.46 | +8.9% | 28.75 | -3.6% | 16d | otc |  |  |
| TMC | Basic Materials | 4.51 | 4.44 | -1.5% | 4.83 | +8.8% | 4.03 | -9.3% | 24d | price |  |  |
| TPB | Consumer Defensive | 77.72 | 75.22 | -3.2% | 81.81 | +8.8% | 72.54 | -3.6% | 25d | otc |  |  |
| TDC | Technology | 28.64 | 28.05 | -2.1% | 30.21 | +7.7% | 26.59 | -5.2% | 12d | short |  |  |
| LASR | Technology | 40.29 | 40.06 | -0.6% | 43.10 | +7.6% | 36.58 | -8.7% | 22d | otc | SELL |  |
| KD | Technology | 13.11 | 13.15 | +0.3% | 14.09 | +7.1% | 11.74 | -10.7% | 22d | otc |  |  |
| SGML | Basic Materials | 12.35 | 12.39 | +0.3% | 13.27 | +7.1% | 10.16 | -18.0% | 20d | price | BUY |  |
| WLDN | Industrials | 87.34 | 85.78 | -1.8% | 91.76 | +7.0% | 77.94 | -9.1% | 20d | otc |  |  |
| MLTX | Healthcare | 15.13 | 15.01 | -0.8% | 16.04 | +6.8% | 13.80 | -8.0% | 13d | short | SELL |  |
| CADL | Healthcare | 12.84 | 12.78 | -0.5% | 13.63 | +6.6% | 11.63 | -9.0% | 14d | other | BUY | 09-04 |
| AGYS | Technology | 112.95 | 111.36 | -1.4% | 118.72 | +6.6% | 104.69 | -6.0% | 25d | other |  |  |
| LPL | Technology | 3.27 | 3.30 | +0.9% | 3.49 | +5.8% | 3.01 | -8.9% | 18d | otc |  |  |
| XMTR | Industrials | 91.15 | 92.53 | +1.5% | 97.86 | +5.8% | 76.89 | -16.9% | 21d | other |  |  |
| ABCL | Healthcare | 11.32 | 11.43 | +1.0% | 12.09 | +5.8% | 9.41 | -17.7% | 9d | price | BUY |  |
| RAMP | Technology | 37.82 | 37.75 | -0.2% | 39.86 | +5.6% | 35.36 | -6.3% | 23d | otc |  |  |
| PCT | Industrials | 6.34 | 6.39 | +0.7% | 6.72 | +5.2% | 5.77 | -9.7% | 16d | otc | SELL |  |
| FN | Technology | 402.25 | 407.20 | +1.2% | 428.32 | +5.2% | 343.76 | -15.6% | 13d | short |  |  |
| VIAV | Technology | 34.80 | 34.86 | +0.2% | 36.67 | +5.2% | 31.63 | -9.3% | 16d | otc |  |  |
| CRVS | Healthcare | 14.27 | 14.39 | +0.9% | 15.07 | +4.7% | 10.28 | -28.5% | 12d | otc |  |  |
| HIMX | Technology | 13.41 | 13.68 | +2.0% | 14.32 | +4.7% | 11.93 | -12.8% | 17d | otc |  |  |
| MP | Basic Materials | 53.72 | 54.53 | +1.5% | 56.98 | +4.5% | 47.17 | -13.5% | 18d | otc |  |  |
| NVCR | Healthcare | 17.49 | 17.94 | +2.6% | 18.70 | +4.3% | 15.10 | -15.8% | 27d | other |  |  |
| BRBR | Consumer Defensive | 10.29 | 10.39 | +0.9% | 10.82 | +4.2% | 9.44 | -9.1% | 17d | other |  |  |
| CLVT | Technology | 2.04 | 2.07 | +1.6% | 2.15 | +4.1% | 1.90 | -8.3% | 29d | other | BUY |  |
| REAX | Real Estate | 18.29 | 18.67 | +2.1% | 19.32 | +3.5% | 8.24 | -55.9% | 29d | price | BUY |  |
| STX | Technology | 813.91 | 849.28 | +4.3% | 878.15 | +3.4% | 734.33 | -13.5% | 25d | other |  |  |
| CSIQ | Technology | 12.75 | 13.22 | +3.7% | 13.61 | +3.0% | 11.84 | -10.5% | 11d | price | SELL | 09-04 Watch/IMPAIRED |
| VSEC | Industrials | 198.18 | 203.91 | +2.9% | 208.19 | +2.1% | 180.06 | -11.7% | 9d | otc |  |  |
| AMKR | Technology | 45.71 | 47.77 | +4.5% | 48.76 | +2.1% | 40.01 | -16.2% | 21d | other |  |  |
| LEU | Energy | 168.26 | 173.89 | +3.3% | 177.29 | +2.0% | 154.11 | -11.4% | 20d | otc |  |  |
| VYX | Technology | 8.73 | 9.14 | +4.7% | 9.17 | +0.4% | 8.32 | -9.0% | 30d | otc |  | 09-04 |

---

## How to use this

1. Section A is a data-integrity fix, not a trade.
2. Sections B and C are the model's own timing telling you the move is spent or late.
3. Section D is the live set. Within it, the 11 grounded names carry real DD; the rest
   are screen-score-only -> UNVERIFIED.
4. No sizing and no entry price given — there is none in the file, and size/price/timing
   are the PM's. The live broker screen remains the veto.
