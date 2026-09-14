# Buying decisions — $50,000 deployment tranche (rev 2)

**Tranche date:** 2026-09-13 · **Revised:** 2026-09-14 · **Supersedes**
`buy_decisions_20260913.md` (7 orders)

**Mandate:** deploy $50,000 from the $600,000 money market into deep-discount alpha++ names,
existing or new · **Sizing cap:** raised from $2,500 to $4,000 (SMALL); HALF reads $2,000 ·
**Screen:** `input/demand_converge.tsv` asof ~2026-09-07

Every name below was **grounded by the PM**. Nothing here was grounded by Claude. All levels,
sizes and exits are the PM's.

---

## 0. Sizing convention — settled 2026-09-14

**"Add X to $Nk" means the position's target MARKET VALUE, not its cost basis.** PM's call.

Room-to-size is always `$Ncap − current_market_value`. The cap is a **target exposure**, not a
capital-at-risk budget, so a position that has fallen gets topped up *more* — averaging down is
the intended behaviour and matches this tranche's deep-discount mandate. This is also the basis
the PM's own over-cap analysis already used (57 positions / $204,426 / 40.5%), so the book now
carries one basis rather than two.

Cost basis survives in exactly one place: the gain constraint `hi = G/(1+G)` in the stop spec,
where `G` is by definition a return on cost. **Sizing uses market value; stops use cost.**

---

## 1. Itemised buys — 10 orders, $16,347.95

All are GTC limits parked **below** market, so the 2026-09-16 FOMC acts as a fill mechanism
rather than a timing risk. That structure is the PM's, from the RKLB order.

| # | name | company | limit | sh | dollars | type | target |
|---|---|---|---|---|---|---|---|
| 1 | RKLB | Rocket Lab | $59.00 | 25 | $1,475.00 | add | — |
| 2 | COHU | Cohu | $53.00 | 28 | $1,484.00 | open | — |
| 3 | MRAM | Everspin Technologies | $15.25 | 98 | $1,494.50 | open | — |
| 4 | SPIR | Spire Global | $10.25 | 146 | $1,496.50 | open | — |
| 5 | VTS | Vitesse Energy | $16.50 | 90 | $1,485.00 | open | — |
| 6 | AIRJ | AirJoule Technologies | $3.85 | 207 | $796.95 | open | — |
| 7 | ETOR | eToro Group | $28.00 | 53 | $1,484.00 | open | — |
| 8 | PENG | Penguin Solutions | $48.00 | 59 | $2,832.00 | **add** | to $4,000 |
| 9 | ENTG | Entegris | $135.00 | 20 | $2,700.00 | **add** | to $4,000 |
| 10 | FLY | Firefly Aerospace | $20.00 | 55 | $1,100.00 | **add** | to $2,000 |
| | | | | | **$16,347.95** | | |

**Capital: $50,000 − $16,347.95 = $33,652.05 uncommitted.**

**Weighted beta of placed dollars: 2.94.**

| sector | dollars | share |
|---|---|---|
| Technology | $8,510.50 | **52.1%** |
| Industrials | $4,868.45 | 29.8% |
| Energy | $1,485.00 | 9.1% |
| Financial Services | $1,484.00 | 9.1% |

**Names with beta > 3: $11,098.00 = 67.9% of placed dollars**, going into Wednesday's FOMC
(~69% CME odds of +25bp). VTS at −0.24 is the only order not aligned with that.

### Limit vs. reference price

`liqClose` = `input/liquidty.tsv` Close 2026-09-04 · `dcPx` = `input/demand_converge.tsv` Price
~2026-09-07. Both pre-date every order.

| name | limit | liqClose | dcPx | vs dcPx | vs liqClose |
|---|---|---|---|---|---|
| AIRJ | $3.85 | $4.57 | $4.57 | **−15.8%** | −15.8% |
| ETOR | $28.00 | $32.47 | $32.75 | −14.5% | −13.8% |
| SPIR | $10.25 | $11.98 | $11.98 | −14.4% | −14.4% |
| RKLB | $59.00 | $64.26 | $64.26 | −8.2% | −8.2% |
| FLY | $20.00 | $21.67 | $21.67 | −7.7% | −7.7% |
| PENG | $48.00 | $51.76 | $51.76 | −7.3% | −7.3% |
| VTS | $16.50 | $17.78 | $17.41 | −5.2% | −7.2% |
| MRAM | $15.25 | $16.37 | $15.85 | −3.8% | −6.8% |
| ENTG | $135.00 | $138.74 | $130.70 | **+3.3%** ⚠ | −2.7% ⚠ |
| COHU | $53.00 | $50.72 | $45.98 | **+15.3%** ⚠ | +4.5% ⚠ |

**Two exceptions, both flagged to the PM when placed:**

- **COHU $53 is above both references** — 4.5% above the 09-04 close, 15.3% above the 09-07
  print. Unless COHU traded through $53 after 09-07, that order fills immediately at the ask
  rather than on weakness.
- **ENTG $135 straddles the two references** — 2.7% *below* the 09-04 close but 3.3% *above* the
  09-07 print. Genuinely ambiguous; which is nearer current decides whether it waits for
  weakness.

The live broker screen (step 7) settles both and is the PM's veto. Noted, not contested.

---

## 2. Passed grounding, no price instruction — 10 names

Nothing is parked on these.

INDI · SIDU · TGTX · CERS · CRMD · ROOT · EVGO · SG · EZPW · ANDG

## 3. Still awaiting grounding — 13 names, all existing holdings

ALT · MTSI · BAND · ACMR · NOK · PUMP · MRP · EE · TRU · SUPV · ASTS · HIMX · LRCX

All 16 new names from the screen are dispositioned. Of the 16 held add candidates, 3 are priced
(PENG, ENTG, FLY) and 13 remain. Eight of the 13 are Technology (MTSI, BAND, ACMR, NOK, ASTS,
HIMX, LRCX and — by industry — none other), so working down the list in score order concentrates
the tranche further. The low-beta diversifiers among them are MRP 0.78, EE 0.45, TRU 0.95 and
PUMP 0.94.

---

## 4. Stop-protectability — every priced name

Under `spec_gain_protect_buffer_rev2.md` §7.4, `lo = max(0.03, 8 × SIGMA20)` and
`hi = min(0.30, G/(1+G))`; when `lo > hi` the spec emits `UNPROTECTABLE, Action = NONE` and
writes no stop. Because `hi` can never exceed `hi_abs = 0.30`, any name whose daily sigma exceeds
**3.75 percentage points** is unprotectable at *every* gain level.

| name | daily σ | `8 × σ` | verdict | min gain to arm |
|---|---|---|---|---|
| VTS | 2.04pp | 16.3% | **protectable** | +19.4% |
| ETOR | 3.30pp | 26.4% | **protectable** | +35.9% |
| ENTG | 4.29pp | 34.3% | unprotectable | — |
| COHU | 4.20pp | 33.6% | unprotectable | — |
| PENG | 5.17pp | 41.4% | unprotectable | — |
| AIRJ | 5.88pp | 47.1% | unprotectable | — |
| RKLB | 5.99pp | 47.9% | unprotectable | — |
| SPIR | 6.54pp | 52.3% | unprotectable | — |
| FLY | 6.98pp | 55.9% | unprotectable | — |
| MRAM | 7.24pp | 57.9% | unprotectable | — |

**2 of 10.** Eight of the ten orders are discretionary exits from the moment they fill.

Among the names that passed grounding but carry no price: EZPW (2.62pp → 21.0%, arms at +26.6%)
and TGTX (2.86pp → 22.9%, +29.7%) are also protectable. ANDG 31.5%, CRMD 31.6%, EVGO 32.9%,
ROOT 33.7%, SG 37.9%, CERS 40.0%, INDI 43.1% and SIDU 96.7% are not.

This is the `hi_abs` finding from `decisions_20260907.md`: **0.30 is a value Claude chose, not one
the PM derived**, and it — not the gain constraint — is the binding term across the high-beta
sleeve, affecting an estimated 101 of 239 trading-book names. Open decision for spec §15.

**Sigma caveat.** `liquidty.tsv`'s `Volatility` column is computed over `DataDays` (median 2,763
sessions), **not** 20, and its definition is undocumented. These sigmas **proxy** the spec's
`SIGMA20` and are **UNVERIFIED**. The structural result is arithmetic and holds regardless of
source; only the thresholds move.

---

## 5. Short-interest direction — a blind spot in the screen

The bounce-back score's `FUEL` term uses `C_Short(%flt)` **magnitude only**. It reads neither
`C_ShortChg(%)` (growing or shrinking?) nor days-to-cover (how fast can it clear?), so a
shrinking short on a long cover and a building short on a 2-day cover score identically.

| name | short %flt | chg % | DTC | reading |
|---|---|---|---|---|
| ANDG | 23.8 | **−14.6** | 6.62 | covering hardest |
| SPIR | 10.3 | −10.5 | 6.25 | covering |
| ROOT | 15.3 | −10.0 | 5.32 | covering |
| ENTG | 5.2 | −9.4 | 3.40 | covering, but no size |
| PENG | 12.8 | −6.2 | 4.05 | covering |
| VTS | 21.3 | −5.7 | 11.88 | covering, longest cover — **best profile** |
| RKLB | 8.0 | −3.1 | 2.18 | covering |
| INDI | 31.6 | −2.8 | 8.04 | covering |
| SIDU | 24.8 | −2.6 | 3.41 | covering |
| EVGO | 33.2 | −0.9 | 10.43 | flat, highest short % |
| FLY | 11.0 | +1.6 | 3.21 | building, 3-day cover — **no fuel** |
| MRAM | 18.1 | +1.6 | 2.44 | building |
| AIRJ | 18.1 | +2.0 | 2.66 | building, fast cover — **overstated** |
| TGTX | 22.3 | +2.7 | 12.59 | building |
| EZPW | 22.9 | +4.2 | 10.54 | building |
| CRMD | 25.9 | +5.3 | 11.05 | building |
| COHU | 19.4 | +10.3 | 9.68 | building |
| SG | 23.1 | +11.7 | 2.88 | building, fast cover — **overstated** |
| CERS | 8.9 | +15.8 | 5.07 | building |
| ETOR | 5.7 | +24.4 | 2.23 | building, from a small base |

**Candidate fix:** weight `FUEL` by `−C_ShortChg(%)` and by days-to-cover. Not applied — it would
re-rank the 13 held names still awaiting grounding, and that re-rank is the PM's call.

---

## 6. Notable per-name factor profiles

- **PENG** — strongest accumulation leg in the whole exercise: `A_NetFlow +134.14%`,
  `A_NewCt 103` vs `A_ClosedCt 20` (**5.2×**), `A_Mgrs 279`, against `D_RSI 3.5`, `D_VEL 94.7`,
  `D_DIST 100.0` (maximum).
- **ENTG** — institutional heavyweight: `A_Mgrs 510`, the largest of any name touched;
  `A_NewCt 103` vs 45; `DVOL $296.4m`; `DataDays 6,578` (~26 years).
- **VTS** — the only order whose short book was shrinking on a *long* cover (−5.73% on 11.88
  days), and the only one that is both protectable and negative-beta.
- **AIRJ** — best new/closed ratio among the new names (29 vs 12, 2.4×) but shorts building on a
  2.66-day cover.
- **FLY** — `D_RSI 0.1`, maximally washed; `A_NewCt 69` vs 27; `DataDays 272` (~13 months), the
  shortest history of any name touched.

---

## 7. Caveats carried by the whole tranche

1. **Nothing on the screen was grounded by Claude.** WEN and QDEL both cleared structurally
   identical screens and died on grounding. The factor files **cannot distinguish accumulation
   from liquidation** — WEN's OTC spike was dated four days *after* its collapse.
2. **`demand_converge.tsv` is asof ~2026-09-07 — six sessions stale — and RSI/VEL are the entire
   ranking.**
3. **The short leg is worse.** `demand_converge.C_DTC` reproduces
   `short_aggregate.latest_days_to_cover` exactly on every name checked, so the C leg rests on a
   **single source settling 2026-08-14 — 30 days stale.** The apparent cross-file agreement is
   propagation, not confirmation.
4. **FOMC Wednesday 2026-09-16, ~69% odds of +25bp**, against 67.9% of placed dollars in beta > 3.
5. **Biotech cluster.** TGTX + CERS + CRMD passed grounding into a Healthcare sleeve already at
   **35 names / $83,185 / 16.5% of the $504,502 trading book, 27 of 35 negative**. The PM stated
   Paula's catalyst calendar is the right instrument for biotech timing and deferred it to next
   week; these three would go on before it exists.
6. **Thin tier**, DVOL under $10m: CERS $5.2m, EVGO $5.2m, SPIR $7.2m, VTS $7.2m, AIRJ $7.2m.
   Dilution risk is invisible to the factor files — the raw-filing step carries the weight.
7. **Short price history**, `DataDays` far under the book median of 2,763: FLY 272 (~13 months),
   ANDG 180, ETOR 331, VTS 917, AIRJ 1,153. Betas and vols rest on less data than they imply.
8. **AIRJ data oddities, UNVERIFIED:** `PE` 33.7 on a $331m market cap, and `Industry` reads
   "Building Products & Equipment," which looks like a misclassification.
9. **ALT** (still ungrounded) has 294 sh — the entire position — under open 5%
   TrailingStopLimits in ROTH 1 (98 sh, VVO-254) and IRA 2 (196 sh, VVX-248). Shares added there
   are unprotected until the order quantity is extended.
10. **Zero overlap with the prealpha 111.** Different model, different failure mode; this is not
    a second opinion on that list.

---

*Nothing in this file is an order or a recommendation to trade. Levels, sizes and every exit
remain the PM's. Companion record: `decisions_20260907.md`, 2026-09-13 and 2026-09-14 entries.*
