# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** |Azure | M | Document every place the field-mapping suggestion feature would call the provider directly, to confirm the dependency stays contained to one service, not scattered across the codebase|
| **Abstraction** |Abstraction Layer - build mapping suggestion calls that go through this interface.  | H |Build the single interface every mapping-suggestion call goes through, so nothing else in the code imports the vendor SDK directly |
| **Routing** | A config setting lets mapping suggestion field point at a different HIPAA-compliant model without a code change; not yet automated | M | Add a basic rule (e.g. "if the eval flags a regression, fall back to Model B automatically") so routing doesn't require a human to notice and flip the switch|
| **Eval** |	No automated test set exists to confirm a replacement model is good enough before switching | H | 	Build a 50-pair regression set (real source-field → canonical-field examples with known right answers) and a script that scores any candidate model against it |

## Portability Score
<!-- Ready / Partial / Locked --> The core reconciliation engine (rules, precedence, conflict detection, RSR/ADR export) has zero AI dependency and would keep working through any provider issue. The field-mapping suggestion feature specifically is not abstracted or eval-tested yet, so a forced switch there today would be a scramble, not a flip of a setting.

## If [primary vendor] doubles pricing tomorrow:
<!-- What's your 48-hour response? --> No immediate runtime cost shock — suggestions run once per system per agency at onboarding, not per transaction. The real cost is that new-agency onboarding gets pricier, and it forces the abstraction-layer / eval work to happen under pressure.

## If [primary vendor] ships a competing product:
<!-- What's defensible that they can't replicate? --> What's defensible and can't be replicated by a better model: each agency's saved crosswalk configuration, their Field Authority precedence rules (their own trust decisions, encoded into the tool), and the actual Epic/CAREWare/case-management integration work already built and tested for that agency. None of that lives in the model — it's the workflow layer.
