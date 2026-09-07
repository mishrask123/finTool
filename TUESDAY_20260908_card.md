# Tuesday 2026-09-08 — pre-open candidate card

**Built 2026-09-07 (Labor Day, market closed) from the three mm_* model files only.**
`*.run.tsv` ignored per PM — stale cache of older runs.

## Sources (quote file + row on every number)
| Input | Path | asof | rows |
|---|---|---|---|
| levels/entries | `poc/20260902/mm_prealpha/invest.tsv` | **2026-08-31 (Mon)** | 111 |
| micro model | `poc/20260902/mm_micro/predict.tsv` | 2026-09-02 (Wed) | 560 |
| ETF blend | `poc/20260902/mm_micro/etf.tsv` | 2026-09-02 (Wed) | 893 |
| price re-strike | `input/eod_price.tsv` | 2026-09-05 (Sat stamp) = **Fri 09-04 close** | 7,706 |

⛔ **invest.tsv is asof Mon 08-31 — 5 sessions before Tuesday.** Every `limit_px`
and `stop_loss_px` below was struck off 08-31 spot and has been RE-CHECKED here
against the Friday 09-04 close. All 111 tickers resolved a Friday close; none missing.

⛔ No sizing given — PM owns size/price/timing ([[feedback-no-sizing-no-pricing]]).
⛔ Long-only card. No exits or cuts proposed ([[feedback-dont-push-cuts]]).

---

## A. DATA INTEGRITY — 3 broken stops, do not place as-is

`stop_loss_px` sits **at or above** Friday's close. Placed as written these fire
instantly at a loss. Stale-stop wiring is the most critical failure mode
([[lessons-broker-pipeline]]).

| TICKER | Sector             | FriClose |    Limit | vsLimit |     Stop | StopDist | Prob | 20dTgt | Source        | Micro |
|---|---|---|---|---|---|---|---|---|---|---|
| ASAN   | Technology         |     8.81 |    10.32 |  -14.7% |     8.94 |    +1.4% | 0.83 | +10.4% | OTC_SPIKE     | - |
| BAND   | Technology         |    43.77 |    54.03 |  -19.0% |    47.34 |    +8.2% | 1.00 | +15.2% | OTC_SPIKE     | - |
| CRDO   | Technology         |   170.57 |   211.65 |  -19.4% |   174.45 |    +2.3% | 0.70 | +15.1% | VOLUME_SPIKE  | - |

---

## B. LIVE ENTRIES — Friday close still at/below limit (68 names, micro model not opposed)

| TICKER | Sector             | FriClose |    Limit | vsLimit |     Stop | StopDist | Prob | 20dTgt | Source        | Micro |
|---|---|---|---|---|---|---|---|---|---|---|
| REPL   | Healthcare         |    15.04 |    20.12 |  -25.3% |     8.90 |   -40.8% | 1.00 | +66.3% | OTC_SPIKE     | BUY |
| ETSY   | Consumer Cyclical  |    76.51 |    88.29 |  -13.3% |    73.53 |    -3.9% | 1.00 | +17.0% | OTC_SPIKE     | - |
| CADL   | Healthcare         |    12.78 |    13.63 |   -6.2% |    11.63 |    -9.0% | 1.00 | +13.3% | OTC_SPIKE     | BUY |
| VYX    | Technology         |     9.14 |     9.17 |   -0.4% |     8.32 |    -9.0% | 0.99 | +10.4% | OTC_SPIKE     | - |
| GPRE   | Basic Materials    |    15.45 |    15.98 |   -3.3% |    13.02 |   -15.7% | 0.98 | +18.0% | OTC_SPIKE     | - |
| ACLS   | Technology         |   115.08 |   116.79 |   -1.5% |   100.64 |   -12.5% | 0.97 | +12.1% | OTC_LED       | - |
| BWXT   | Industrials        |   157.59 |   171.70 |   -8.2% |   150.09 |    -4.8% | 0.97 | +13.3% | OTC_SPIKE     | - |
| SONO   | Technology         |    15.36 |    16.00 |   -4.0% |    13.78 |   -10.3% | 0.97 | +12.3% | OTC_SPIKE     | - |
| STX    | Technology         |   849.28 |   878.15 |   -3.3% |   734.33 |   -13.5% | 0.97 | +17.2% | VOLUME_SPIKE  | - |
| TNDM   | Healthcare         |    19.90 |    22.63 |  -12.1% |    18.82 |    -5.4% | 0.97 | +13.5% | OTC_SPIKE     | - |
| DXC    | Technology         |    11.66 |    11.71 |   -0.4% |    10.52 |    -9.8% | 0.96 | +10.4% | OTC_SPIKE     | - |
| ACHR   | Industrials        |     5.72 |     5.90 |   -3.0% |     5.06 |   -11.6% | 0.96 | +12.1% | OTC_SPIKE     | - |
| ABCL   | Healthcare         |    11.43 |    12.09 |   -5.5% |     9.41 |   -17.7% | 0.95 | +15.0% | VOLUME_LED    | BUY |
| IESC   | Industrials        |   322.57 |   395.21 |  -18.4% |   221.47 |   -31.3% | 0.85 | +72.8% | OTC_SPIKE     | - |
| EVCM   | Technology         |     7.92 |     8.62 |   -8.1% |     7.37 |    -6.9% | 0.85 | +13.9% | OTC_SPIKE     | - |
| CENX   | Basic Materials    |    46.78 |    50.32 |   -7.0% |    41.79 |   -10.7% | 0.85 | +16.2% | OTC_SPIKE     | - |
| SMCI   | Technology         |    39.59 |    42.31 |   -6.4% |    29.26 |   -26.1% | 0.85 | +33.5% | OTC_LED       | BUY |
| CNXC   | Technology         |    32.16 |    34.37 |   -6.4% |    29.53 |    -8.2% | 0.85 | +13.5% | OTC_SPIKE     | BUY |
| OMER   | Healthcare         |    18.95 |    20.01 |   -5.3% |    17.78 |    -6.1% | 0.85 | +15.0% | OTC_LED       | BUY |
| FN     | Technology         |   407.20 |   428.32 |   -4.9% |   343.76 |   -15.6% | 0.85 | +13.4% | VOLUME_SPIKE  | - |
| BTSG   | Healthcare         |    60.73 |    63.57 |   -4.5% |    52.59 |   -13.4% | 0.85 | +16.0% | OTC_SPIKE     | - |
| NVCR   | Healthcare         |    17.94 |    18.70 |   -4.1% |    15.10 |   -15.8% | 0.85 | +14.7% | HOLDING_SPIKE | - |
| CLVT   | Technology         |     2.07 |     2.15 |   -3.9% |     1.90 |    -8.3% | 0.85 | +11.7% | VOLUME_SPIKE  | BUY |
| AMKR   | Technology         |    47.77 |    48.76 |   -2.0% |    40.01 |   -16.2% | 0.85 | +14.0% | VOLUME_SPIKE  | - |
| LPL    | Technology         |     3.30 |     3.49 |   -5.5% |     3.01 |    -8.9% | 0.85 | +14.0% | OTC_SPIKE     | - |
| SGML   | Basic Materials    |    12.39 |    13.27 |   -6.6% |    10.16 |   -18.0% | 0.85 | +15.8% | VOLUME_SPIKE  | BUY |
| BFLY   | Healthcare         |     7.36 |     8.94 |  -17.7% |     7.05 |    -4.2% | 0.85 | +21.8% | OTC_SPIKE     | - |
| CRVS   | Healthcare         |    14.39 |    15.07 |   -4.5% |    10.28 |   -28.5% | 0.84 | +12.3% | OTC_SPIKE     | - |
| HIMX   | Technology         |    13.68 |    14.32 |   -4.5% |    11.93 |   -12.8% | 0.84 | +14.4% | OTC_SPIKE     | - |
| QURE   | Healthcare         |    44.50 |    49.98 |  -11.0% |    36.40 |   -18.2% | 0.84 | +12.0% | VOLUME_SPIKE  | - |
| LEU    | Energy             |   173.89 |   177.29 |   -1.9% |   154.11 |   -11.4% | 0.84 | +11.0% | VOLUME_LED    | - |
| GFI    | Basic Materials    |    47.40 |    48.46 |   -2.2% |    40.23 |   -15.1% | 0.84 | +17.9% | OTC_SPIKE     | - |
| SQM    | Basic Materials    |    76.43 |    84.64 |   -9.7% |    75.25 |    -1.5% | 0.84 | +10.7% | OTC_SPIKE     | BUY |
| HPK    | Energy             |     8.05 |     8.55 |   -5.8% |     7.42 |    -7.8% | 0.83 | +11.6% | OTC_SPIKE     | - |
| BRBR   | Consumer Defensive |    10.39 |    10.82 |   -4.0% |     9.44 |    -9.1% | 0.83 | +10.1% | OTC_SPIKE     | - |
| RAMP   | Technology         |    37.75 |    39.86 |   -5.3% |    35.36 |    -6.3% | 0.83 | +11.3% | OTC_SPIKE     | - |
| IE     | Basic Materials    |     9.99 |    10.61 |   -5.8% |     8.95 |   -10.4% | 0.82 | +11.8% | OTC_SPIKE     | - |
| INBX   | Healthcare         |   121.17 |   133.31 |   -9.1% |   111.91 |    -7.6% | 0.82 | +14.9% | OTC_SPIKE     | - |
| IT     | Technology         |   186.42 |   200.99 |   -7.2% |   172.34 |    -7.6% | 0.82 | +12.0% | OTC_SPIKE     | - |
| BRKR   | Healthcare         |    58.50 |    59.23 |   -1.2% |    50.33 |   -14.0% | 0.81 | +12.6% | OTC_SPIKE     | - |
| AGYS   | Technology         |   111.36 |   118.72 |   -6.2% |   104.69 |    -6.0% | 0.81 | +10.5% | OTC_SPIKE     | - |
| KD     | Technology         |    13.15 |    14.09 |   -6.6% |    11.74 |   -10.7% | 0.81 | +15.2% | OTC_SPIKE     | - |
| WEN    | Consumer Cyclical  |     8.03 |     8.69 |   -7.6% |     7.73 |    -3.7% | 0.81 | +10.6% | OTC_SPIKE     | BUY |
| IDCC   | Technology         |   337.94 |   337.96 |   -0.0% |   299.29 |   -11.4% | 0.81 | +11.8% | OTC_SPIKE     | - |
| WLDN   | Industrials        |    85.78 |    91.76 |   -6.5% |    77.94 |    -9.1% | 0.81 | +10.4% | OTC_SPIKE     | - |
| TDC    | Technology         |    28.05 |    30.21 |   -7.2% |    26.59 |    -5.2% | 0.81 | +11.3% | OTC_SPIKE     | - |
| QUBT   | Technology         |     8.01 |     8.56 |   -6.4% |     6.87 |   -14.3% | 0.81 | +17.3% | OTC_SPIKE     | - |
| NAMS   | Healthcare         |    25.40 |    26.25 |   -3.2% |    22.71 |   -10.6% | 0.81 | +10.6% | VOLUME_SPIKE  | - |
| VIAV   | Technology         |    34.86 |    36.67 |   -4.9% |    31.63 |    -9.3% | 0.81 | +11.5% | OTC_SPIKE     | - |
| SOUN   | Technology         |     6.74 |     7.24 |   -7.0% |     5.97 |   -11.4% | 0.80 | +11.8% | OTC_SPIKE     | - |
| SRPT   | Healthcare         |    22.50 |    22.58 |   -0.3% |    18.66 |   -17.1% | 0.80 | +14.1% | OTC_SPIKE     | BUY |
| PINS   | Communication Services |    20.40 |    22.59 |   -9.7% |    19.10 |    -6.4% | 0.70 | +13.0% | OTC_SPIKE     | - |
| XMTR   | Industrials        |    92.53 |    97.86 |   -5.5% |    76.89 |   -16.9% | 0.70 | +15.7% | OTC_SPIKE     | - |
| MBX    | Healthcare         |    61.72 |    65.04 |   -5.1% |    54.15 |   -12.3% | 0.70 | +14.8% | OTC_SPIKE     | - |
| QDEL   | Healthcare         |    13.97 |    14.71 |   -5.0% |    12.53 |   -10.3% | 0.70 | +14.2% | OTC_SPIKE     | - |
| REAX   | Real Estate        |    18.67 |    19.32 |   -3.4% |     8.24 |   -55.9% | 0.70 | +17.0% | VOLUME_SPIKE  | BUY |
| FDX    | Industrials        |   322.52 |   358.52 |  -10.0% |   289.49 |   -10.2% | 0.70 | +22.1% | OTC_LED       | - |
| VSEC   | Industrials        |   203.91 |   208.19 |   -2.1% |   180.06 |   -11.7% | 0.69 | +10.5% | OTC_SPIKE     | - |
| IBRX   | Healthcare         |     8.08 |     8.32 |   -2.9% |     7.12 |   -11.9% | 0.68 | +12.9% | OTC_SPIKE     | - |
| STOK   | Healthcare         |    29.81 |    32.46 |   -8.2% |    28.75 |    -3.6% | 0.68 | +10.5% | OTC_SPIKE     | - |
| MP     | Basic Materials    |    54.53 |    56.98 |   -4.3% |    47.17 |   -13.5% | 0.68 | +12.6% | OTC_SPIKE     | - |
| DOW    | Basic Materials    |    29.44 |    32.15 |   -8.4% |    27.80 |    -5.6% | 0.68 | +11.7% | VOLUME_SPIKE  | - |
| MTRN   | Basic Materials    |   244.24 |   246.83 |   -1.0% |   214.04 |   -12.4% | 0.68 | +11.5% | OTC_SPIKE     | - |
| TMC    | Basic Materials    |     4.44 |     4.83 |   -8.1% |     4.03 |    -9.3% | 0.68 | +14.8% | VOLUME_SPIKE  | - |
| MUX    | Basic Materials    |    20.07 |    20.28 |   -1.0% |    17.52 |   -12.7% | 0.67 | +12.9% | OTC_SPIKE     | - |
| WGS    | Healthcare         |    85.99 |    90.25 |   -4.7% |    77.75 |    -9.6% | 0.66 | +13.4% | OTC_SPIKE     | - |
| SEDG   | Technology         |    34.20 |    35.65 |   -4.1% |    27.85 |   -18.6% | 0.66 | +21.3% | OTC_SPIKE     | - |
| TPB    | Consumer Defensive |    75.22 |    81.81 |   -8.1% |    72.54 |    -3.6% | 0.66 | +10.7% | OTC_SPIKE     | - |

---

## C. LIVE BUT MICRO MODEL SAYS SELL (13 names) — conflict, treat as UNVERIFIED

invest.tsv says BUY, predict.tsv says SELL on the same name. Two models of the same
book disagreeing is not a lead — resolve on the tape before acting.

| TICKER | Sector             | FriClose |    Limit | vsLimit |     Stop | StopDist | Prob | 20dTgt | Source        | Micro |
|---|---|---|---|---|---|---|---|---|---|---|
| CSIQ   | Technology         |    13.22 |    13.61 |   -2.9% |    11.84 |   -10.5% | 1.00 | +13.8% | VOLUME_SPIKE  | SELL |
| AMPX   | Industrials        |     9.89 |    10.51 |   -5.9% |     8.10 |   -18.1% | 0.85 | +23.6% | OTC_SPIKE     | SELL |
| PRIM   | Industrials        |    74.43 |    77.51 |   -4.0% |    62.77 |   -15.7% | 0.85 | +15.5% | OTC_SPIKE     | SELL |
| IONQ   | Technology         |    39.52 |    40.61 |   -2.7% |    32.45 |   -17.9% | 0.85 | +15.7% | OTC_SPIKE     | SELL |
| RUN    | Technology         |     8.89 |     9.01 |   -1.3% |     7.20 |   -19.0% | 0.85 | +16.5% | OTC_SPIKE     | SELL |
| RGTI   | Technology         |    15.20 |    16.06 |   -5.4% |    12.32 |   -19.0% | 0.84 | +14.7% | OTC_SPIKE     | SELL |
| QBTS   | Technology         |    16.58 |    17.78 |   -6.8% |    13.47 |   -18.7% | 0.83 | +15.8% | OTC_LED       | SELL |
| RCAT   | Industrials        |     8.37 |     9.05 |   -7.5% |     6.70 |   -20.0% | 0.83 | +20.6% | OTC_SPIKE     | SELL |
| PCT    | Industrials        |     6.39 |     6.72 |   -5.0% |     5.77 |    -9.7% | 0.83 | +12.4% | OTC_SPIKE     | SELL |
| EYE    | Consumer Cyclical  |    16.74 |    17.58 |   -4.8% |    15.60 |    -6.8% | 0.82 | +10.7% | OTC_SPIKE     | SELL |
| LASR   | Technology         |    40.06 |    43.10 |   -7.1% |    36.58 |    -8.7% | 0.70 | +14.7% | OTC_SPIKE     | SELL |
| MLTX   | Healthcare         |    15.01 |    16.04 |   -6.4% |    13.80 |    -8.0% | 0.69 | +12.5% | VOLUME_SPIKE  | SELL |
| FLNC   | Utilities          |    10.35 |    11.75 |  -11.9% |     9.02 |   -12.8% | 0.68 | +26.4% | OTC_SPIKE     | SELL |

---

## D. ALREADY RAN — Friday close ABOVE limit (27 names) — DO NOT CHASE

The move largely happened between 08-31 and 09-04. Per [[feedback-real-dd-method]]
the tape vetoes the memo: a catalyst already in the price is a PASS, not an entry.
Note the cluster — crypto miners / power (RIOT CIFR HUT IREN BTDR CORZ MARA) moved
together, which is basket beta, not 7 idiosyncratic edges.

| TICKER | Sector             | FriClose |    Limit | vsLimit |     Stop | StopDist | Prob | 20dTgt | Source        | Micro |
|---|---|---|---|---|---|---|---|---|---|---|
| EOSE   | Industrials        |     3.88 |     3.23 |  +20.2% |     2.49 |   -35.9% | 0.70 | +20.8% | OTC_SPIKE     | - |
| HUT    | Financial Services |    93.54 |    81.46 |  +14.8% |    69.32 |   -25.9% | 0.70 | +11.3% | OTC_SPIKE     | - |
| RIOT   | Financial Services |    21.80 |    19.34 |  +12.7% |    15.10 |   -30.7% | 0.85 | +19.1% | OTC_SPIKE     | - |
| IREN   | Financial Services |    44.68 |    39.96 |  +11.8% |    31.56 |   -29.4% | 0.81 | +15.6% | VOLUME_SPIKE  | - |
| BE     | Industrials        |   252.87 |   226.76 |  +11.5% |   181.86 |   -28.1% | 0.85 | +14.0% | OTC_SPIKE     | - |
| CIFR   | Technology         |    17.74 |    15.92 |  +11.4% |    12.56 |   -29.2% | 0.85 | +19.5% | OTC_SPIKE     | - |
| BTDR   | Technology         |    12.38 |    11.52 |   +7.5% |     8.73 |   -29.5% | 0.85 | +22.6% | VOLUME_SPIKE  | - |
| ALMS   | Healthcare         |    11.10 |    10.38 |   +7.0% |     8.51 |   -23.3% | 0.70 | +22.7% | OTC_SPIKE     | SELL |
| ASTS   | Technology         |    62.31 |    58.50 |   +6.5% |    47.84 |   -23.2% | 0.98 | +13.2% | OTC_SPIKE     | - |
| DAVE   | Technology         |   380.69 |   359.82 |   +5.8% |   309.98 |   -18.6% | 0.85 | +13.9% | OTC_SPIKE     | - |
| CORZ   | Technology         |    17.89 |    16.92 |   +5.8% |    14.32 |   -19.9% | 0.84 | +11.6% | OTC_SPIKE     | SELL |
| FOUR   | Technology         |    45.93 |    43.47 |   +5.7% |    37.86 |   -17.6% | 0.81 | +12.8% | OTC_SPIKE     | - |
| AEHR   | Technology         |    86.26 |    82.79 |   +4.2% |    64.96 |   -24.7% | 0.70 | +18.1% | OTC_SPIKE     | SELL |
| MARA   | Financial Services |    11.31 |    10.90 |   +3.8% |     7.84 |   -30.7% | 0.85 | +13.9% | OTC_SPIKE     | BUY |
| PENG   | Technology         |    51.76 |    50.02 |   +3.5% |    42.87 |   -17.2% | 0.84 | +13.0% | OTC_SPIKE     | - |
| GCT    | Technology         |    51.75 |    50.14 |   +3.2% |    44.16 |   -14.7% | 0.85 | +11.3% | VOLUME_SPIKE  | - |
| OPK    | Healthcare         |     1.64 |     1.59 |   +3.1% |     1.28 |   -21.8% | 0.80 | +18.7% | VOLUME_SPIKE  | - |
| ALGT   | Industrials        |    78.16 |    75.99 |   +2.9% |    65.38 |   -16.4% | 0.67 | +10.4% | OTC_LED       | - |
| HLF    | Consumer Defensive |    12.38 |    12.13 |   +2.0% |    10.77 |   -13.0% | 1.00 | +11.3% | VOLUME_SPIKE  | - |
| SOFI   | Financial Services |    18.22 |    17.94 |   +1.6% |    15.52 |   -14.8% | 0.81 | +11.0% | OTC_SPIKE     | - |
| AXTI   | Technology         |    61.64 |    60.69 |   +1.6% |    48.13 |   -21.9% | 0.84 | +18.7% | OTC_SPIKE     | - |
| ICHR   | Technology         |    56.38 |    55.64 |   +1.3% |    46.65 |   -17.2% | 0.85 | +15.2% | VOLUME_LED    | SELL |
| LUMN   | Communication Services |     6.77 |     6.71 |   +0.8% |     5.68 |   -16.1% | 0.70 | +11.7% | OTC_SPIKE     | - |
| SANM   | Technology         |   198.47 |   197.63 |   +0.4% |   173.73 |   -12.5% | 0.81 | +11.6% | OTC_SPIKE     | - |
| IOVA   | Healthcare         |     8.79 |     8.77 |   +0.2% |     7.06 |   -19.7% | 0.80 | +13.3% | OTC_SPIKE     | BUY |
| HMY    | Basic Materials    |    20.27 |    20.23 |   +0.2% |    18.02 |   -11.1% | 0.70 | +10.9% | OTC_SPIKE     | - |
| STRL   | Industrials        |   486.49 |   486.04 |   +0.1% |   407.31 |   -16.3% | 0.85 | +14.2% | OTC_SPIKE     | - |

