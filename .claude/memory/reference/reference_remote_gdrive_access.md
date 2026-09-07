---
name: reference-remote-gdrive-access
description: "START HERE for any remote/tablet session with no home PC. Google Drive is the durable store: quantbot/tablet/ drop-box, the quantbot/auto layout with folder+file IDs, signal locations, freshness traps (Saturday stamp = Friday close; short/otc aggregates lag their mtime), connector gotchas, and the findings a fresh session cannot re-derive."
metadata:
  type: reference
---
# ⭐ START HERE (remote session, no home PC)

**Everything durable lives in Google Drive. Read this section first, then go straight
to the folder below — do not re-explore Drive from scratch.**

## `quantbot/tablet/` — folder id `1XDQmOTl3BV9de1vL2SbdavNlIt3ZjhMR`
Created 2026-09-07. Sits OUTSIDE `auto/` on purpose so the SOD job never reads it.
This is the PM's tablet drop-box and the durable home for anything Claude produces.

| File | What it is |
|---|---|
| `TUESDAY_20260908_card.md` (id `15HB7mt0zwd-kIDQ-uOkwoVCSqRIha4p2`) | Tue 09-08 pre-open card: 3 broken stops, 68 live entries, 13 model conflicts, 27 already-ran. Levels re-struck vs Fri 09-04 close. |
| `reference_remote_gdrive_access.md` | this file — Drive map, IDs, freshness traps |
| `reference_manual_dd_no_intraday.md` | which DD-gate steps survive with no intraday grounding run |

## 60-second restart recipe

1. Drive connector must be attached (claude.ai Settings -> Connectors). It DOES drop
   mid-session — if a call returns "session expired", re-run ToolSearch on
   `mcp__Google_Drive__*` and retry.
2. Read `quantbot/tablet/` (id above) — the card + these two references.
3. Pull only what the task needs, with `download_file_content` (NEVER
   `read_file_content` for .tsv — it destroys tabs). IDs are in the tables below.
4. The three model files are sufficient for a trading day; `*.run.tsv` is dead cache.

## What a fresh session will NOT know (findings, not files)

Files can be re-pulled in minutes; these conclusions cannot. As of 2026-09-07:
- **CSIQ** — screen prob 1.00 and its top live entry, but grounding says thesis
  IMPAIRED / verdict "Watch" AND predict.tsv says SELL. -> PASS.
- **REPL** — grounded "Strong Entry", thesis INTACT. Cantor Healthcare Conf **Sept 10**
  falls INSIDE the absence window. Its 40.8%-wide stop is deliberate (binary biotech),
  not a data error.
- **BAND / CRDO / ASAN** — `stop_loss_px` sits ABOVE Friday's close; placed as written
  they fire instantly.
- **27 of 111** invest.tsv names already ran past their limit, and the crypto-miner /
  power cluster (RIOT CIFR HUT IREN BTDR CORZ MARA) moved together = basket beta.
- `short_aggregate.tsv` settles at **2026-08-14** and `otc_aggregate.tsv` at
  **2026-09-02**, despite both carrying a Friday 09-04 mtime.
- `mishrask123/finTool` on GitHub is a **PUBLIC** repo.

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
| `input/short_aggregate.tsv` | `1cyuRuOiEyK8NyoVY_ubr0vjxE9sCmKpA` | 09-04 17:07Z |
| `input/otc_aggregate.tsv` | `1HENL_NHFAgEYaBhL5XtpidEPr08K3V5f` | 09-04 17:07Z |
| `input/liquidty.tsv` (has **Beta**) | `18W8qBznWksS5yIBqOVl6EJftRcsB8-gc` | 09-05 05:53Z |
| `input/demand_converge.tsv` | `1kp3qKX-YVlp1usyr0t4WpSHUWkA3v2wZ` | 09-05 03:20Z |
| `pnl/20260904.tsv` (**POSITIONS**, 573 lots) | `1LptBUHHpN3H2TL_xlg9NRRwvDRrn0Wx4` | 09-04 18:32Z |
| `broker/UnrealizedGainLossTaxLots_Realtime.csv` | `1j_dJfPR6UJe6I0_y0okv0ZPmSXfl71Nl` | 09-04 16:35Z |
| `broker/RealizedGainLossTaxLots.csv` | `1uNKcUU6eCmQPsUA-abqAebU44Ok61zgH` | 09-04 15:35Z |
| `broker/open_orders.tsv` (21 open GTC) | `1XPvCw6fpVtTuixxs5CSeSpbl1_DfWWRd` | 09-04 18:32Z |
| `llm/worksheet.tsv` | `1cOHCZuoBfa7Ra34Jph8MavJAQ8oLswZi` | 09-04 17:08Z |
| `llm/worksheet.archive.zip` | `1r8XLyAuHKoLhz4i7j5UG95WnfN1Z2M3i` | 09-04 17:07Z |
| `13f/latest_13f.tsv` | `16v48Z9xKisslR4-rEwNP4v6aKSbVE45V` | 09-05 06:03Z |
| `13f/insider.tsv` | `1rZ16vyrEdEHYbIrzou-EQ-_JHKD8UaHt` | 09-05 06:05Z |
| `portfolio/earnings_estimate_latest.tsv` | `10BvjUUyQtiXJaAphBOcWDPwUeCx_7wR2` | **08-07 — STALE** |

⛔ SKIP `input/price.zip` (id `1_vt233jwViN54VNRVThS9u9UXNaxnjm3`) — **481 MB**, PM
said skip; the connector moves it base64-encoded and it would dominate any transfer.

`pnl/20260904.tsv` columns:
`Date Account SubAccount Symbol Qty AvgCost Price DeltaPct Vol MktCap Basket
MktValue PnL_Pct PnL_Dollar ManagementType Action LotDate`

STALE WARNING: `earnings_estimate_latest.tsv` is a month old. It is the only
earnings-date source, and the absence plan calls an unattended GTC filling into
an earnings print the main risk. Any earnings date derived from it -> UNVERIFIED.

FRESHNESS TRAP — ALWAYS resolve a date to its DAY OF WEEK before trusting it.
2026: Aug-31 Mon, Sep-02 Wed, Sep-03 Thu, Sep-04 Fri, Sep-05 **Sat**, Sep-06 Sun,
Sep-07 Mon (US Labor Day, market CLOSED), Sep-08 Tue.

The SOD pipeline runs early SATURDAY morning and stamps files with the Saturday
date while carrying **Friday's close**. `eod_price.tsv` rows all read
`2026-09-05 01:48:24` = Sat 01:48 EDT => contents are the **Fri 09-04 close**,
which IS the correct EOD reference for the Tue 09-08 pre-open (Mon 09-07 is a
holiday, so Friday is the last completed session). Do NOT mistake the Saturday
stamp for stale data. `equity_px.txt` was checked ticker-by-ticker against
`eod_price.tsv` and MATCHES exactly — same Friday close, no newer data hides in it.

⚠️ mtime lies on the aggregates: `short_aggregate.tsv` has
`latest_settlement_date` maxing at **2026-08-14** (FINRA bi-monthly lag, ~3 weeks)
and `otc_aggregate.tsv` `latest_asofdate` at **2026-09-02** (Wed) — both despite a
Friday 09-04 mtime. `liquidty.tsv` IS genuinely fresh: 7,000 rows asof 09-04.

Internal stamp beats Drive mtime, but read both: mtime tells you when the file was
written, the internal date tells you which session it covers.

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
5. WRITING to Drive: `create_file` with `textContent` +
   `disableConversionToGoogleType: true` (else markdown becomes a Google Doc).
   Content passes through context, so only SMALL text files are practical to write
   back. Raw pipeline files are ALREADY on Drive — never round-trip them.
6. The connector session expires mid-run. Re-run ToolSearch on
   `mcp__Google_Drive__*` and retry; nothing is lost.

## ⛔ IGNORE `*.run.tsv` (PM, 2026-09-07)

`ALPHA.run.tsv`, `DISCLOSURE.run.tsv`, `EMERGING.run.tsv`, `MEAN_REV.run.tsv`,
`ACCUM.run.tsv`, `MERGER.run.tsv`, `DILUTION.run.tsv` under `poc/<date>/` are a
**cache of older runs** — NOT current signal. Do not read them, do not cite them,
do not build cards from them. They also carry no date column, so they cannot be
aged. PM: "ignore *.run.tsv they are cache of older run".

⭐ The **three `mm*/*.tsv` files are sufficient** for a trading day:
`mm_prealpha/invest.tsv`, `mm_micro/predict.tsv`, `mm_micro/etf.tsv`.

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

### asofdate audit (checked 2026-09-07) — only eod_price is Saturday-current

| File | internal asofdate | day | Drive mtime | day |
|---|---|---|---|---|
| `input/eod_price.tsv` | 2026-09-05 01:48:24 | **Sat** (= Fri close) | 09-05 05:49Z | Sat |
| `mm_micro/predict.tsv` | 2026-09-02 | Wed | 09-03 13:03Z | Thu |
| `mm_micro/etf.tsv` | 2026-09-02 | Wed | 09-03 13:03Z | Thu |
| `mm_prealpha/invest.tsv` | 2026-08-31 | **Mon** | 09-03 07:14Z | Thu |
| `poc/20260903/ALPHA.run.tsv` | (no date col) | — | 09-04 16:59Z | Fri |
| `poc/20260902/ALPHA.run.tsv` | (no date col) | — | 09-03 20:01Z | Thu |

⛔ Only the price file is Saturday-current. The model outputs are NOT: invest.tsv is
asof Mon 08-31 (a full week before Tue 09-08) and predict/etf are asof Wed 09-02.
`ALPHA.run.tsv` carries NO date column at all — its only provenance is the poc
folder name plus Drive mtime. Any limit_px / stop_loss_px taken from invest.tsv is
priced off week-old spot and MUST be re-checked against eod_price.tsv before use.

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
