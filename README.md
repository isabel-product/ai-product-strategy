# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

# Ai Product Strategy

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

- **Product:** RyFlow, AI Mapping automator for Ryan White Programs
- **AI Value Archetype:** Automator/Oracle
- **Vulnerability Scores:** _(add: Moat 3/5 · Data 2/5 · Platform 3/5)_
- **Top Risk:** Data Advantage is the weakest axis — RyFlow's real defensibility depends on turning single-agency field mappings into a cross-agency crosswalk library over time.
- **Confidence:** M
- **Prototype:** https://lovable.dev/projects/36b5e54d-64f8-4c42-b912-a444d611bc61?magic_link=mc_c5037949-a9e4-43ca-9a09-f5149f2804a6
- **Kill Criteria:** if 3+ target agencies say their manual reconciliation burden is under 5 hours/quarter, or if CAREWare's own roadmap includes native multi-system reconciliation within 12 months, the bet doesn't hold.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:**
- **Weakest Loop:** Preference Loop
- **Top Encroachment Threat:** HRSA/HAB's own CAREWare product team
- **Encroachment Defense:** Currently, we are not considering tracking preference of field authority. However preference of which field should be the trusted source for the reporting layer (RSR/ADR reports) can be tracked and ke…
- **Vendor Portability:** The core reconciliation engine (rules, precedence, conflict detection, RSR/ADR export) has zero AI dependency and would keep working through any provider issue. The field-mapping suggestion feature specifically is not abstracted or eval-tested yet, so a forced switch there today would be a scramble, not a flip of a setting.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):**
- **Gross Margin (AI-adjusted):**
- **Pricing Model:** Hybrid to include a base fee per agency (covering integration setup and maintenance) plus usage (number of reconciled records).
- **Pricing Today → Tomorrow:** **Proposed AI pricing:** Not priced as a separate line item. → Not priced as a separate line item.
- **Total AI COGS / unit:**
- **Cascading Strategy:** Triage: A small, cheap classification model handles the default case — matching a source field name/sample values to one of ~20-30 canonical RSR/ADR fields. This is not a task requiring frontier intelligence.; frontier: Reserved only for low-confidence matches the triage model can't resolve cleanly — e.g., ambiguous or unusually-named fields where a stronger model's broader pattern recognition might close the gap before falling back to "map by hand."; ratio ~90-95% handled by the triage model, ~5-10% escalated to frontier — most field names are recognizable enough (patient.dob, client.race) that they don't need heavier reasoning.
- **Net Margin Shift:** Earning more revenue due to the metered addition which scales revenue with the size of clients.
- **Break-even at:**

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** 90%
- **Golden Dataset:** 10 rows, __ adversarial
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

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** **The case:**
- **Ask:** ## M1 Baseline vs. Now
- **Key Strategic Change:**

→ Details: [`06-the-pitch/`](06-the-pitch/)

