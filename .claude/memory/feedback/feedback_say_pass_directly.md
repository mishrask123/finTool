---
name: feedback-say-pass-directly
description: "When the signal does not hold up, say PASS outright. Do not bury the verdict in a size discussion or an options menu."
metadata:
  type: feedback
---

# Say PASS directly

PM 2026-09-07: *"be direct tell pass when signal not good"*.

⛔ Do NOT answer a size question ("half size?") with a conditional like "not HALF —
SMALL or nothing". That reads as a qualified buy. If the signal fails, the answer is
**PASS**, stated first, then the reason.

Concrete miss that triggered this: TNDM. Asked "half size?", the reply led with size-class
reasoning (beta 1.06 so HALF's risk-cut rationale does not apply -> "SMALL or nothing")
and left the actual verdict — PASS — buried at the end. PM had to ask "are you saying
small buy $2500?" to extract it.

Rule:
1. Lead with **BUY** or **PASS**. One word, first line.
2. Size only after a BUY, and only when asked ([[feedback-no-sizing-no-pricing]]).
3. A size question is not permission to skip the verdict.

Same family as [[lessons-broker-pipeline]] BEHAVIORAL: when PM says clean/fix/do, JUST DO
IT — no option-menus, no hedging, lead with the action.

## Signal-fails triggers that mean PASS on sight

- The signal's own engine contradicts it (e.g. `OTC_SPIKE` with a NEGATIVE `otc`
  attribution, or OTC flow below its average) — TNDM: otc -0.2734, flow 0.65x.
- Target already met / exceeded at the current close.
- Predicted peak (PeakT from asofdate) already passed.
- `stop_loss_px` at or above the current close.
- Ungrounded (not in the 44-name Gemini cache) AND no `predict.tsv` corroboration.
