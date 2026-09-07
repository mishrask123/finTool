---
name: reference-remote-gdrive-access
description: "How to reach the trading pipeline's data from a REMOTE session (tablet/web, no home PC). Google Drive connector layout, folder/file IDs, freshness, connector gotchas, and the local mirror. Written 2026-09-07 during the 09-06..09-20 absence."
metadata:
  type: reference
---

# Remote data access — Google Drive (no home PC)

Context: PM is away 2026-09-06 -> 09-20 with a tablet + broker portals only
([[project-vacation-absence-2wk]]). The Windows toolchain (`ps\recon`, `calc_size`,
`worksheet_set`, C#/.NET) CANNOT run remotely. Drive is the substitute: read the
same files the pipeline writes, analyse them locally with awk/python.

## Drive layout — `quantbot/auto/` is the working root

`G:` on the home PC == Google Drive. Everything for the work is under `auto/`.

| Path | Folder ID |
|---|---|
| `quantbot` | `1Zv7MWbqprHyv0Se9GO-gDYujQTcxhPDc` |
| `quantbot/auto` | `12m1W13YA7law0GU3T4AKCW3AzbwbdE4B` |
| `auto/input` | `1QFqrINyPYOMszdy5au2xlGnuihCxbN_8` |
| `auto/poc` | `1gMMDVtJGchWefwUlCIQVtJj8pmU4jmp_` |
| `auto/broker` | `11xHZzfHCzrPsjuiIsWdhv8CUKqdBYKi1` |
| `auto/llm` | `1IOnBCskFEyzU3W6eC1rHCbRbg70W3PDF` |
| `auto/portfolio` | `1aZ2OwjWvep9lRktsksTHOASOy01UQ1rN` |
| `auto/report` | `1ijHAzCzwopyM5PEWJEXxnNKegeU-7anM` |
| `auto/pnl` | `12fdRiSGw46UDm7R4jEYiMsGnI6lh47Sp` |
| `auto/13f` | `1ostc9x87_-z3fTB15txqcXkUGMnqSiwr` |
| `auto/risk` | `1JITcYwz6QBOL16MLzLoEBjS6QjJbHCKB` |
| `auto/log`, `auto/logs` | `1-paLa97wn_q7wKA9XRjBX9Khjdl0IXDL`, `1z6p72AmvG7yZnA5ogpDB97Z74f5V7Xje` |
| `auto/config` | `1bZ3XhVwy7aalq8d3BBeDMbbwgH8aZbY6` |
| `auto/portfolio/gemini_cache/order2` | `1vzCnv2x6F0Qtj4sd5dFBGINwo-8bUjZb` |

Other `auto/` children: commands, energy, faq, research, intraday, temp, prompts,
investment, mapping, etf, edgar.

## Signals live in `auto/poc/<DATE>/`

One folder per data date (written the NEXT morning), each holding the signal run
files. Only two dates present as of 2026-09-07: **20260902** and **20260903**.
20260903 is the freshest -> that is the actionable set.

`{SIGNAL}.run.tsv` where SIGNAL = ALPHA, DISCLOSURE, EMERGING, MEAN_REV, ACCUM,
MERGER, DILUTION. Sibling folders: `mm_insider`, `mm_prealpha`, `mm_equity`,
`mm_etf`, `mm_run`, `mm_micro`, `mm_13f`, `mm_mean_rev`.

| Date | Folder ID | ALPHA.run.tsv ID |
|---|---|---|
| 20260903 | `1whYijn2c5Kr8XgEbPbYASTWoqw9oFm7W` | `1wAIPMNBQsvxRzc-i7jvSVSdYw893zoEn` |
| 20260902 | `1A5FabWXSmKT-EaozhCqrGqPXwDmBLKTE` | `1TmPLFRZ5_4P2Wx9KiXornmBm9aQNM4ig` |

`ALPHA.run.tsv` columns (19):
`MODEL_NAME SYMBOL SUB_MODEL NAME STATUS REASON PRICE MKTCAP SECTOR INDUSTRY
DIRECTION MAX_RETURN TRADESCORE DECISION CONFIDENCE VOLUME SMOOTH EAR DD`

## Key file IDs + freshness (as of 2026-09-07)

| File | ID | Modified |
|---|---|---|
| `input/eod_price.tsv` | `1xolxaDb_xOh8csS8N9Utf2cU4vRkSlUL` | 09-05 05:49Z |
| `input/equity_meta.txt` | `14yFxNmC-0y8Q4KEKVuIf4RExfK4Ny1eO` | 09-05 21:29Z |
| `input/equity_px.txt` | `1SVbQ2J7mbHvRdWGlvJFVDepF_ISo4_nX` | 09-05 21:29Z |
| `input/early_alpha.tsv` | `1m5bAoP4utQD9M3tlLw2hLe1IZXK_pKKo` | 09-05 21:29Z |
| `broker/UnrealizedGainLossTaxLots_Realtime.csv` | `1j_dJfPR6UJe6I0_y0okv0ZPmSXfl71Nl` | 09-04 16:35Z |
| `broker/RealizedGainLossTaxLots.csv` | `1uNKcUU6eCmQPsUA-abqAebU44Ok61zgH` | 09-04 15:35Z |
| `broker/open_orders.tsv` | `1XPvCw6fpVtTuixxs5CSeSpbl1_DfWWRd` | 09-04 18:32Z |
| `llm/worksheet.tsv` | `1cOHCZuoBfa7Ra34Jph8MavJAQ8oLswZi` | 09-04 17:08Z |
| `llm/worksheet.archive.zip` | `1r8XLyAuHKoLhz4i7j5UG95WnfN1Z2M3i` | 09-04 17:07Z |
| `13f/latest_13f.tsv` | `16v48Z9xKisslR4-rEwNP4v6aKSbVE45V` | 09-05 06:03Z |
| `13f/insider.tsv` | `1rZ16vyrEdEHYbIrzou-EQ-_JHKD8UaHt` | 09-05 06:05Z |
| `portfolio/earnings_estimate_latest.tsv` | `10BvjUUyQtiXJaAphBOcWDPwUeCx_7wR2` | **08-07 — STALE** |

STALE WARNING: `earnings_estimate_latest.tsv` is a month old. It is the only
earnings-date source, and the absence plan calls an unattended GTC filling into
an earnings print the main risk. Any earnings date derived from it -> UNVERIFIED.

FRESHNESS TRAP: `eod_price.tsv` rows all carry an internal stamp of
`2026-09-05 01:48:24` (EDT, ~01:48 Friday) => it holds the **09-04 THURSDAY close**,
NOT Friday's. `equity_px.txt` was written 09-05 17:29 EDT (after Friday's close) and
may carry Friday. Always read the internal timestamp, never trust Drive's mtime.

## Connector gotchas (IMPORTANT)

1. `read_file_content` is **LOSSY** for data files: it converts every TAB to a
   single SPACE and markdown-escapes text (`MODEL\_NAME`, `\<`). Since fields
   contain spaces ("Alcoa Corporation", "EV & Solar"), TSV columns become
   UNRECOVERABLE. Never use it for .tsv/.csv.
2. `download_file_content` returns base64 and is **BYTE-EXACT** (verified:
   437,056 bytes in == 437,056 out, all tabs intact). Use this for all data files.
3. Oversized results are spilled by the harness to a local file under
   `tool-results/` and do NOT enter context. So LARGE files are cheaper to fetch
   than small ones. Decode with:
   `python3 -c "import json,base64;d=json.load(open(SPILL));open(OUT,'wb').write(base64.b64decode(d['content']))"`
   (`read_file_content` spills use key `fileContent` and are plain text, not base64.)
4. Small files return inline and must be re-emitted to reach disk — costly. Prefer
   batching / fetching only what is needed.

## ⭐ The three folders that matter most (PM, 2026-09-07)

PM named **mm_prealpha, mm_micro, macro** as the most important. Status:

| Folder | Where | Contents | Status |
|---|---|---|---|
| `mm_prealpha` | `poc/20260902/` id `13Z6SKJOskShh11DvgOPINvW5wfMTBZM9` | `invest.tsv` 60,848 B, 111 rows | HAVE |
| `mm_micro` | `poc/20260902/` id `1DeWoeoEzMD_8Q8FNAbOyR0kb3A-UdK7i` | `predict.tsv` 211,654 B / 560 rows; `etf.tsv` 764,436 B / 893 rows | HAVE |
| `macro` | — | — | ⛔ DOES NOT EXIST IN DRIVE |

⛔ **macro**: no folder anywhere in Drive named macro/mm_macro. The ONLY match for
"macro" is `config/FILTER/macro_fwd_return.tsv` (id `19AilAfiZApNGeM0fPIlG_L30oPbAohQ1`,
19 bytes) whose entire content is a threshold config, not data:
`Key<TAB>Value` / `MIN<TAB>0.15`. The repo carries `specs/macro-report-business-spec-v1.md`
and `specs/macro-report-sample-v1.tex`, so macro reporting looks SPECIFIED BUT NOT
YET PRODUCED. Ask PM where macro output lands before assuming it is missing.

⚠️ **Both live under 20260902, NOT the newer 20260903.** The 20260903 folder contains
only the 7 `*.run.tsv` files plus `mm_insider` — the mm_* model outputs were not
regenerated on 09-03. So mm_prealpha/mm_micro are one day older than ALPHA.run.tsv.

### Schemas

`mm_prealpha/invest.tsv` (37 cols) — per-name trade card, the closest thing to a
ready-to-act sheet:
`key asofdate ticker direction name sector market_cap liquidity spot_px limit_px
stop_loss_px pred_target_px_20d pred_target_px_20dpct adj_pred_target_px_20d
adj_pred_target_px_20pct shap_fwd20_ret aumc smooth ear dd r2 rmse prob strategy
source intelligence reason price liq short otc other cross_otc_x_short
cross_otc_x_liq cross_price_x_otc cross_price_x_short cross_trend_x_liq`
⭐ Carries **limit_px and stop_loss_px per name** — directly usable from a broker
portal with no tooling.

`mm_micro/predict.tsv` (29 cols) — per-ticker 20d prediction:
`ticker asofdate step action curve_type spot_price target_price max_return aumc
train_r2 train_rmse prob_score smooth ear dd otc_shap liquid_shap short_squeeze
absorption volume_confirmed_momentum flow_imbalance otc_price_divergence
relative_volume_vs_index otc_short_conflict short_exhaustion liquidity_shock
otc_z short_z missing_frac`

`mm_micro/etf.tsv` (48 cols) — predict.tsv schema plus ETF component-blend fields
(`comp`, `tot_comp_*`, `etf_mm_score`, `component_count`, `long/short/hold_count`,
`net_assets`, `dollar_theoretical_move`, `theoretical_qty`). Note `comp` packs
multiple components into one cell delimited by `^` with `comp=TICKER|weight|score`
triples — parse, do not split naively.

Local mirror: `/home/user/gdrive/poc/20260902/mm_prealpha/`, `.../mm_micro/`.

## Local mirror (this container, EPHEMERAL)

`/home/user/gdrive/` mirrors the Drive paths:
- `input/eod_price.tsv` (via read_file_content — space-mangled, adequate ONLY
  because no field contains a space; re-pull with download_file_content if in doubt)
- `poc/20260903/ALPHA.run.tsv` (byte-exact, 2,111 rows)
- `poc/20260902/ALPHA.run.tsv` (byte-exact, 3,105 rows)
- `poc/20260902/mm_prealpha/invest.tsv` (byte-exact, 111 rows)
- `poc/20260902/mm_micro/predict.tsv` (byte-exact, 560 rows)
- `poc/20260902/mm_micro/etf.tsv` (byte-exact, 893 rows)

The container is reclaimed after inactivity — anything worth keeping must be
committed and pushed.

## Repo access from remote

- `mishrask123/sachi` — attached READ-ONLY at `/home/user/sachi` (shallow clone,
  HEAD `63a627c` "save" 2026-09-05). Its `.claude/memory/` is the canonical doctrine
  and IS recoverable this way. Cannot push without re-attaching with write access.
- `mishrask123/finTool` — writable, working branch `tactical`. This file lives here
  because sachi is read-only; fold it into sachi's `.claude/memory/reference/` when
  write access is available.
