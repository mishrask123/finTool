---
name: reference-manual-dd-no-intraday
description: "DD when there is NO intraday grounding run (PM absence 2026-09-06..09-20, tablet + broker portals only). Which of the 7 DD-gate steps are still satisfiable off static .tsv on Drive, what substitutes for the memo, and the Gemini grounding cache that survives."
metadata:
  type: reference
---

# Manual DD off .tsv — no intraday grounding run

PM 2026-09-07: "we will not have intraday run that does grounding, we will manually
work off the .tsv". So `recon --gemini`, fresh memos under `intraday\{sym}.md`, and
PPX/Gemini grounding are ALL unavailable. DD must be reconstructed from static files.

⛔ This weakens the gate. [[feedback-real-dd-method]] still binds: a screen score is a
LEAD, not a decision. Where a step cannot be run, say **UNVERIFIED** — never infer it.

## The 7-step gate ([[reference-dd-7-steps]]) under absence

| # | Step | Status | Substitute |
|---|---|---|---|
| 1 | memo `intraday\{sym}.md` | ⛔ no new memos | **Gemini cache** below, for 44 names only |
| 2 | `short_aggregate.tsv` (% of FLOAT, not %chg) | ✅ `input/short_aggregate.tsv` id `1cyuRuOiEyK8NyoVY_ubr0vjxE9sCmKpA` 3.9MB, **Fri 09-04 17:07Z** | — |
| 3 | `otc_aggregate.tsv` fresh flow | ✅ `input/otc_aggregate.tsv` id `1HENL_NHFAgEYaBhL5XtpidEPr08K3V5f` 712KB, **Fri 09-04 17:07Z** | — |
| 4 | 13F top holders | ✅ `13f/latest_13f.tsv`, `latest_13f_raw.zip`, `insider.tsv` (09-05) | — |
| 5 | `recon_order --rsi --buy --watch` | ⛔ cannot run | approximate RSI/DIST/tape from `input/eod_price.tsv` + `equity_meta.txt`; call it UNVERIFIED, it is NOT the screen |
| 6 | raw filing .txt.html | ⚠️ EDGAR fetch may work over the proxy; untested | `edgar/` folder on Drive; else UNVERIFIED |
| 7 | live broker screen | ✅ PM-only, via portal | unchanged — still the real veto |

Also still available: `broker/open_orders.tsv` (GTC book), `RealizedGainLossTaxLots.csv`
(harvested -> don't re-chase), `UnrealizedGainLossTaxLots_Realtime.csv` (positions).

## ⭐ The Gemini grounding CACHE survives — 44 tickers

`auto/portfolio/gemini_cache/order2/` holds per-ticker grounded memos as
`{TICKER}_{MODEL}.json` (+ the `.prompt` that produced them). These are REAL
grounding — catalyst, thesis, risk flags, verdict, sourced and dated — and they do
NOT need the intraday run. This is the ONLY memo substitute available.

| Sub-folder | id | asof | tickers |
|---|---|---|---|
| `PreAlpha` | `1x3mmhmpY4-iT3TCSkysoN6cwtHzBukuO` | 2026-09-04 | ACHC AON APLD APTV BAND BEKE CADL CSIQ EIX ETSY FROG GPCR HLF HPP HSAI HWM MNSO NVTS OABI PCG REPL RIG RXRX RYAN SPRY VYX WING ZS ZURA |
| `PreAlpha_Otc` | `1yYZTocUPEnEQMrbutK1cf3Z5ZvkLcvzM` | 2026-09-03 | ACHR AMPX APP APPS AUTL HUN IOVA OI PLTK QUAD RDW RPD SEDG ULCC |
| `PreAlpha_Volume` | `1Jb2TnZr59kucAAmt-saSv1XBHOMHvWQM` | 2026-09-03 | BLMN |
| `PreAlpha_Holding` | `1H4lVmNM_xRSTLAsIyEy9CaMcUb2ZLcp0` | 2026-09-03 | FROG |

JSON fields: `catalyst_confirmed`, `catalyst_reason`, `thesis_intact`
(INTACT/IMPAIRED), `thesis_reason`, `risk_flags`, `gemini_verdict`
(Strong Entry / Watch / ...), `sector_validated`, `crypto_risk`,
`wash_trading_risk`, `sourceRef`, `shortReason`, `asofDate`, `fetchedAt`,
`realtimePx`.

⚠️ Only **11 of the 111** `invest.tsv` names are covered: ACHR AMPX BAND CADL CSIQ
ETSY HLF IOVA REPL SEDG VYX. The other 100 have NO grounding available at all —
they are screen-score-only and must be called UNVERIFIED.

## Worked examples (2026-09-07) — the cache overturns the screen

**CSIQ** — invest.tsv `prob 1.00`, its top live entry. Grounding says
`thesis_intact: "IMPAIRED"`, verdict **"Watch"**: *"Q2 results showed a massive EPS
miss (-$1.40 vs. -$0.74 expected) and soft Q3 guidance due to US factory ramp-up
costs and pricing pressure."* `predict.tsv` independently says **SELL**. Three
sources, two against -> PASS. The highest-scoring name on the card is the one not
to buy.

**REPL** — `prob 1.00`, verdict **"Strong Entry"**, `thesis_intact: "INTACT"`:
FDA accelerated approval for TUDRIQEV (Aug 6), $150M August financing for runway.
Risk: *"Ongoing securities class action lawsuits; accelerated approval contingent on
future confirmatory trial results (IGNYTE-3)."*
⚠️ EVENT IN ABSENCE WINDOW: Cantor Healthcare Conference **Sept 10**.

## Standing rule while manual

1. Screen score alone is never a BUY — it is a lead.
2. If the name is in the 44-cache, read the memo and QUOTE it. If not, mark UNVERIFIED.
3. Re-strike every `limit_px`/`stop_loss_px` against the latest `eod_price.tsv`
   before it goes near a portal — invest.tsv levels are asof Mon 08-31.
4. Cross-check `invest.tsv` BUY against `predict.tsv` action; a SELL there is a conflict.
5. Step 7 (live broker screen) remains the PM's and is still the real veto.
