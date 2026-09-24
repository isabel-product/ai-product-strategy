# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

# RyFlow is an AI-driven data-integration and quality layer that reconciles client and encounter records across a Ryan White program's clinical, case management, and reporting systems so staff can stop manually de-duplicating data and trust what they submit for required federal reporting. RyFlow produces clean, de-duplicated, cross-validated data ready for RSR (Ryan White Services Report) and ADR (Annual Data Report) submission. The core pain it targets: program staff currently do manual de-duplication and re-key the same client/encounter data into multiple systems, which erodes data quality and burns staff time every reporting cycle.

> Ryan White program data teams will pay for a reconciliation layer that turns their EHR, lab, case-management, and CAREWare reporting data into one trusted source, because manual de-duplication is currently a recurring, auditable, quantifiable cost center for every grantee.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [x] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** RyFlow is an AI-driven data-integration and quality layer that reconciles client and encounter records across a Ryan White program's clinical, case management, and reporting systems so staff can stop manually de-duplicating data and trust what they submit for required federal reporting. RyFlow produces clean, de-duplicated, cross-validated data ready for RSR (Ryan White Services Report) and ADR (Annual Data Report) submission. The core pain it targets: program staff currently do manual de-duplication and re-key the same client/encounter data into multiple systems, which erodes data quality and burns staff time every reporting cycle.
- **AI Value Archetype:** Automator/Oracle
- **Vulnerability Scores:** _(Moat 3/5 · Data 2/5 · Platform 3/5)_
- **Top Risk:** Data Advantage is the weakest axis — RyFlow's real defensibility depends on turning single-agency field mappings into a cross-agency crosswalk library over time.
- **Confidence:** M
- **Prototype:** https://lovable.dev/projects/36b5e54d-64f8-4c42-b912-a444d611bc61?magic_link=mc_c5037949-a9e4-43ca-9a09-f5149f2804a6
- **Kill Criteria:** if 3+ target agencies say their manual reconciliation burden is under 5 hours/quarter, or if CAREWare's own roadmap includes native multi-system reconciliation within 12 months, the bet doesn't hold.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 7-10/20
- **Weakest Loop:** Preference Loop
- **Top Encroachment Threat:** HRSA/HAB's own CAREWare product team
- **Encroachment Defense:** Currently, we are not considering tracking preference of field authority. However preference of which field should be the trusted source for the reporting layer (RSR/ADR reports) can be tracked and ke…
- **Vendor Portability:** The core reconciliation engine (rules, precedence, conflict detection, RSR/ADR export) has zero AI dependency and would keep working through any provider issue. The field-mapping suggestion feature specifically is not abstracted or eval-tested yet, so a forced switch there today would be a scramble, not a flip of a setting.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** 63.7%
- **Gross Margin (AI-adjusted):** 72.1%
- **Pricing Model:** Hybrid to include a base fee per agency (covering integration setup and maintenance) plus usage (number of reconciled records). A base fee per agency ($400/month, covering integration setup and maintenance) plus usage (number of client records reconciled per cycle, at $0.15/record). At a mid-size agency (800 records/month), this lands at ~$520/month and lifts gross margin from 63.7% (flat-fee baseline) to 72.1%, since the metered component scales revenue with agency size the same way real infrastructure and storage cost already does.
- **Pricing Today → Tomorrow:** None yet, no live product. For modeling purposes, the reference point used elsewhere in this doc is a flat $400/month per agency, which yields 63.7% gross margin at a mid-size agency's $145.28 real cost basis. → Not priced as a separate line item. AI inference (field-mapping suggestions) costs under $0.30/agency/month even at the higher end of usage — negligible relative to the $145.28 total cost basis, which is dominated by infrastructure and storage, not AI. Breaking AI out as its own priced line would add complexity without capturing meaningful additional value; it's bundled into the base fee as part of the core platform.
- **Total AI COGS / unit:** $145.28/agency/month
- **Cascading Strategy:** Triage: A small, cheap classification model handles the default case — matching a source field name/sample values to one of ~20-30 canonical RSR/ADR fields. This is not a task requiring frontier intelligence.; frontier: Reserved only for low-confidence matches the triage model can't resolve cleanly — e.g., ambiguous or unusually-named fields where a stronger model's broader pattern recognition might close the gap before falling back to "map by hand."; ratio ~90-95% handled by the triage model, ~5-10% escalated to frontier — most field names are recognizable enough (patient.dob, client.race) that they don't need heavier reasoning.
- **Net Margin Shift:** Earning more revenue due to the metered addition which scales revenue with the size of clients. At the mid-size agency's $145.28 cost basis, moving from flat $400 to metered $520 lifts gross margin fr…
- **Break-even at:**  Will likely need to fund this as a strategic loss-leader or R&D investment because the standalone P&L won't clear break-even at realistic scale.

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** 90%
- **Golden Dataset:** 10 rows, 6 adversarial
- **Confidence UX:** Tiered confidence with a hard human-in-the-loop trigger at the bottom tier.
- **HITL Architecture:** Confidence below 50%, or any adversarial-pattern match (sensitive-identifier-shaped field, suspected prompt injection, or no-signal input) → no auto-suggestion is shown at all; the field routes straight to manual mapping with an on-call eng…
- **Failure Mode Coverage:** *What failure mode did your partner find that you missed?* composite/derived canonical fields — like eUCI being built from patient.mrn + patient.dob rather than mapped from a single source field — aren't represented anywhere in the current …

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales, and what compounds.**

- **Compounding System:** | Loop | Input | Output | Compounds? | Status | |------|-------|--------|-----------|--------| | Recursive Learning|A reviewer accepting or overriding a field-mapping suggestion |Confidence score shown for other suggeste…
- **Governance Posture:** AI-assisted features within the RyFlow product — specifically, field-mapping suggestions during system integration setup, and the confidence-scoring/reconciliation-recommendation logic in the Field Authority and Reconcil…
- **Autonomy Boundaries:** Suggesting a field mapping (High confidence, >90%), auto. Accepting a field mapping into the agency's live crosswalk config (Medium confidence, 70-90%), human approval required.…
- **Escalation Triggers:** 1. Suggestion confidence <70% 2. A field's sample values match a sensitive-identifier pattern (SSN-like formats) 3. Detected prompt-injection pattern in source field content 4.…
- **Audit Cadence:** Weekly, Automated eval of current model/prompt version against the golden dataset (accuracy + hallucination-rate metrics from the Reliability Contract) (Development/Engineering Lead).…
- **Shadow AI Audit (user-side):**
- **Agent Boundaries:** Not applicable.
- **Regulatory Exposure:** HIPAA (client health and identity data flows through every part of this product). Risk tier: limited. Controls: Signed BAA required with every connected system's host organization (per the non-functional requirements).…

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):** Persist Field Authority precedence rules per agency to a real production database · Build the abstraction layer (suggestField()) so every AI suggestion call routes through one interface, not scattered vendor SDK calls · Build the 50-pair golden dataset and wire it into CI as a deploy gate (block if accuracy <85% or hallucination >5%) · Ship tiered confidence UX: Accept + Override always available, Accept hidden below 70% confidence · Implement cascading model routing: lightweight model handles routine field matches, escalate low-confidence cases to a stronger model once, then fall back to manual · Onboard first 2-3 design-partner agencies on read-only Epic + CAREWare integration
- **Horizon 2 (Next):** Build the shared, system-type-keyed crosswalk library across agencies · Confirm real export/API capabilities for Provide Enterprise, Lifia Portal, and RWise, and ship at least one working connector · Launch hybrid pricing (base fee + per-record-reconciled metering) with design-partner agencies · Stand up the quarterly governance review and shadow-AI audit process using real agency usage data (not the earlier hypothetical audit)
- **Horizon 3 (Bet):** Pilot write-back to one low-risk source system (e.g., case management, not Epic) for confirmed reconciled values · Pilot the reconciliation pattern with a non-Ryan-White federally-reported health program facing a similar multi-system data-quality problem
- **Board Narrative:** Ryan White programs already trust us for CAREWare-adjacent work — RyFlow turns a manual data-reconciliation burden they already have into a natural extension of a relationship we already own.
- **Ask:** 2 engineers and 1 PM for a 6-month window, with a hard checkpoint at that point to decide whether this continues, scales, or folds back into the core product line.…
- **Key Strategic Change:** At a realistic ceiling of ~24 agencies, RyFlow covers only ~17% of a 2-engineer-plus-PM team's fixed cost, not break-even. The ask to leadership has to shift from "fund this because the unit economics work" to an explicit choice: either justify it as a strategic investment (stickiness for the existing CAREWare-adjacent product line, a foothold for a later adjacent-market bet, or eventual positioning as infrastructure worth acquiring rather than competing against) and accept the loss, or right-size the team to match the realistic agency ceiling — likely 1 engineer, not 2.

→ Details: [`06-the-pitch/`](06-the-pitch/)

