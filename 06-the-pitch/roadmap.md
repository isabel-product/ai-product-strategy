# Three-Horizon Roadmap & Board Pitch

## Roadmap


### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
|Persist Field Authority precedence rules per agency to a real production database | Bet| H |
|Build the abstraction layer (suggestField()) so every AI suggestion call routes through one interface, not scattered vendor SDK calls |Guardrails |H|
|Build the 50-pair golden dataset and wire it into CI as a deploy gate (block if accuracy <85% or hallucination >5%) |Contract |H|
|Ship tiered confidence UX: Accept + Override always available, Accept hidden below 70% confidence |Contract |H
|Implement cascading model routing: lightweight model handles routine field matches, escalate low-confidence cases to a stronger model once, then fall back to manual |Margin |H
|Onboard first 2-3 design-partner agencies on read-only Epic + CAREWare integration |**Contract**et |H|

### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Build the shared, system-type-keyed crosswalk library across agencies | Moat |M|
| Confirm real export/API capabilities for Provide Enterprise, Lifia Portal, and RWise, and ship at least one working connector | Bet |M|
| Launch hybrid pricing (base fee + per-record-reconciled metering) with design-partner agencies| Margin |M|
| Stand up the quarterly governance review and shadow-AI audit process using real agency usage data (not the earlier hypothetical audit) | Guardrails |M|

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Pilot write-back to one low-risk source system (e.g., case management, not Epic) for confirmed reconciled values | Bet | L |
| Pilot the reconciliation pattern with a non-Ryan-White federally-reported health program facing a similar multi-system data-quality problem | Moat | L |


(a) the most over-indexed horizon (and what's missing on the others)" H1 is the most over-indexed horizon — six solid execution items (persistence, abstraction layer, golden dataset, confidence UX, cascading router, first agency onboarding), all high-confidence and ready to ship. What's missing elsewhere: H2 has only four bets and none of them touch the Preference loop fix (repeated-override learning) that was already identified as a top priority back in the Compounding System exercise — it's oddly absent from this roadmap despite being one of the cheapest, highest-leverage fixes named earlier. H3 has exactly two items, and one of them (the adjacent-market pilot) is really just "the same bet, different customer," not a genuinely different kind of exploration — there's only one real moonshot on the entire roadmap.
  
(b) the single H3 bet you'd protect if budget got cut: The write-back pilot-- real write risk to systems of record, real compliance exposure, and it directly tests whether RyFlow can become more than a read-only reconciliation layer.

(c) the one initiative I should kill today. Kill the generic "ask AI anything" search bar on the Reconciliation Queue. 
  
## Board Pitch

**Thesis (1 sentence):**

**The case:**
1. Why now:
2. What's defensible:
3. The economics:

**The risks:**
1. Trust / failure modes:
2. Scale / governance:
3. Competitive:

**The ask:**

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:**

**Now:**
