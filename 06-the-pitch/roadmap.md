# Three-Horizon Roadmap & Board Pitch

## Roadmap


### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
|Persist Field Authority precedence rules per agency to a real production database | Bet| H |
|Build the abstraction layer (suggestField()) so every AI suggestion call routes through one interface, not scattered vendor SDK calls |Guardrails |H|
|Build the 50-pair golden dataset and wire it into CI as a deploy gate (block if accuracy <85% or hallucination >5%) |Contract |H|
|Ship tiered confidence UX: Accept + Override always available, Accept hidden below 70% confidence |Contract |H|
|Implement cascading model routing: lightweight model handles routine field matches, escalate low-confidence cases to a stronger model once, then fall back to manual |Margin |H|
|Onboard first 2-3 design-partner agencies on read-only Epic + CAREWare integration |**Contract** |H|

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

**Thesis (1 sentence):** Ryan White programs already trust us for CAREWare-adjacent work — RyFlow turns a manual data-reconciliation burden they already have into a natural extension of a relationship we already own.

**The case:**
1. Why now: This isn't a new market bet, it's a workflow gap sitting directly next to work we already do. Our product line already touches CAREWare and EHR interfaces, so the customer relationship and technical adjacency exist before we build anything new. The pressure to act isn't invented — HRSA's own CAREWare team is the most credible platform threat, and our own kill criteria says this bet doesn't hold if their roadmap ships native multi-system reconciliation within 12 months. That's a real window, not an arbitrary one.
2. What's defensible: Vulnerability scoring today is Moat 3/5, Data 2/5, Platform 3/5 — honestly middling, not a slam dunk. The named weak point is Data Advantage: this is a one-agency-at-a-time tool today, with no cross-agency learning yet. The fix — a shared crosswalk library so agency #50 benefits from what agencies #1-49 already confirmed — is scoped, funded in this ask, and not yet built. 
3. The economics:At a mid-size agency's real cost basis ($145.28/month, mostly infrastructure and integration maintenance, not AI), a flat $400/month subscription yields 63.7% gross margin. Moving to our proposed hybrid model — $400 base plus $0.15 per client record reconciled — lifts that to 72.1%, because pricing now scales with agency size the same way cost already does. AI inference itself is under $0.30/agency/month regardless of pricing model; the margin story here is about pricing structure, not cheaper AI.

**The risks:**
1. Trust / failure modes: The real failure mode is bad data reaching a federal report, not a headline — a wrong RSR/ADR submission has compliance consequences for the grantees we'd serve. Confidence-tiered UX blocks anything below a 70% match from auto-applying, and sensitive-identifier-shaped fields are excluded from suggestions entirely. Our own red-team exercise found a real gap we're not hiding: composite/derived fields (like a client ID built from two source fields) aren't represented in our golden dataset yet.
2. Scale / governance: Our weakest compounding loop today is Preference — the system doesn't yet learn from a reviewer's repeated decisions, so correction #10 on the same recurring conflict looks like correction #1. Governance itself is scoped (weekly automated eval, HIPAA-driven guardrails, confidence-gated autonomy) but hasn't run against real usage yet; standing that up on live data is part of this ask, not something already proven.
3. Competitive: The scenario that forces a kill is CAREWare shipping native reconciliation first, or three-plus target agencies telling us their manual burden is under 5 hours a quarter. Either signal, and we stop rather than keep funding a bet that's stopped holding.

**The ask:** 2 engineers and 1 PM for a 6-month window, with a hard checkpoint at that point to decide whether this continues, scales, or folds back into the core product line. This covers the H1 build-out already scoped (persistence, abstraction layer, golden dataset, confidence UX, cascading routing) and the H2 validation bets (the crosswalk library, confirming real integration capability with three named vendors, launching metered pricing with design partners). What this trades off: those 2 engineers and 1 PM aren't available for 6 months. 

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** An integrator app that maps Ryan White program data across their EHR, lab, case management, and reporting systems, reducing the manual de-duplication and duplicate data entry staff currently do by hand. Classified as an Automator/Oracle blend, with Confidence M and the top risk flagged early as Data Advantage — the product's defensibility would depend on turning single-agency mappings into something that compounds across agencies over time.

**Now:** The same core bet holds, but it's no longer a hunch — it's backed by a working prototype, a named weakest loop (Preference, not just "Data Advantage" in the abstract), a named competitive attacker with a specific mechanism (CAREWare's roadmap, Palantir via a federal-contract path), a real cost model split by actual agency size (small CBO vs. large consortium), and a kill criteria specific enough to act on rather than a vague confidence score. What changed most isn't the bet itself — it's that every soft spot in it now has a name, a number, and a plan attached, instead of being a general risk to keep in mind.
