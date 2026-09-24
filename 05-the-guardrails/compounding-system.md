<img width="626" height="399" alt="image" src="https://github.com/user-attachments/assets/9df87dd8-56f1-46da-b7da-b3e6c0406051" /># Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning|A reviewer accepting or overriding a field-mapping suggestion |Confidence score shown for other suggested fields, same session | Y/N |  missing |
| Cross-Domain Transfer|A confirmed mapping for one canonical field in one system (e.g., Race confirmed in Epic) |Confidence boost for that same canonical field in the agency's other systems (CAREWare, Case Management) | Y/N | / missing |
|Network Intelligence |Confirmed mappings across every agency using the product | Higher starting confidence for a new agency's onboarding on the same system type| Y/N |  missing |

**Broken loop identified by partner:** Recursive Learning. 
**Fix plan:**Right now, when someone accepts or corrects a mapping, that choice only lives in the browser's temporary memory. The fix is to save each correction to an actual database (which agency, which system, which field, what they picked, and when), and make sure the tool actually checks that database before showing a new suggestion, instead of just reacting to what's sitting in memory that moment.

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->
Right now, each agency's corrections stay locked inside that one agency — nothing they fix ever reaches another agency, or any shared system. The silo is that there's no shared place for corrections to land, so knowledge never travels past the agency that created it.

## Governance Policy

**Scope:** AI-assisted features within the RyFlow product — specifically, field-mapping suggestions during system integration setup, and the confidence-scoring/reconciliation-recommendation logic in the Field Authority and Reconciliation Queue screens. Excludes: The rules-based reconciliation engine (Field Authority precedence logic, conflict detection, RSR/ADR export generation) is deterministic, not AI-driven, and is covered under standard software QA, not this policy. Also excludes agency-side systems (Epic, CAREWare, case management platforms) — RyFlow governs its own suggestions and outputs, not how source systems generate or store data.

**Autonomy boundaries:** Suggesting a field mapping (High confidence, >90%), auto. Accepting a field mapping into the agency's live crosswalk config (Medium confidence, 70-90%), human approval required. Resolving a data conflict between systems using the Field Authority precedence rule, human approval required. Mapping any field resembling a sensitive identifier, never auto. Submitting final RSR/ADR export to HRSA, never auto.

**Escalation triggers:** 1. Suggestion confidence <70% 2. A field's sample values match a sensitive-identifier pattern (SSN-like formats) 3. Detected prompt-injection pattern in source field content 4. A composite/derived canonical field (e.g., eUCI built from multiple source fields) 5. Two or more systems disagree on a field value for a real client record

**Audit cadence:** Weekly, Automated eval of current model/prompt version against the golden dataset (accuracy + hallucination-rate metrics from the Reliability Contract) (Development/Engineering Lead). Monthly, Sample of production overrides across agencies, reviewed for drift or emerging edge cases not yet in the golden dataset; override-rate drift check per the Reliability Contract (Product Manager). Quarterly, Full policy review, including a re-check of the composite-field handling and sensitive-identifier exclusions, plus Kill Switch portability re-verification (can we still swap providers) (CISO).

**Regulatory exposure (EU AI Act / other):** HIPAA (client health and identity data flows through every part of this product). Risk tier: limited. Controls: Signed BAA required with every connected system's host organization (per the non-functional requirements). Role-based access controls given data sensitivity. Full audit log of every AI suggestion, human decision, and override, with source and timestamp. Sensitive-identifier fields structurally excluded from the AI suggestion pipeline rather than filtered after the fact..

## Agent Topology

Not applicable.


## Shadow AI Audit

<img width="692" height="239" alt="image" src="https://github.com/user-attachments/assets/7956dc20-cdd6-4a36-92d5-9172ad9c33dd" />

## Discover, User-Side Workarounds
- A data quality lead keeps a personal spreadsheet tracking "which system wins for which field," because the same override keeps getting asked again every reporting cycle | source: Other | signal: Capability gap | freq: H | spend: $0/mo | decision: Build
- Staff at a second agency, hearing informally from a peer agency's data lead which Epic fields map to which RSR categories, manually replicate that mapping by hand instead of getting it suggested | source: Support ticket | signal: Capability gap | freq: H | spend: $0/mo | decision: Build
- An agency exports RyFlow's clean, reconciled data into a separate BI tool (Excel/Power BI) to build local dashboards RyFlow's Reports screen doesn't yet cover | source: Sales call | signal: Pricing gap | freq: L | spend: $50/mo | decision: Partner

## Pattern Assessment
- Workarounds found: 3
- Build candidates: 2
- Partner candidates: 1
- Ignore decisions: 0
- Adjacent spend: $50/mo
- Dominant signal: Capability gap
<img width="722" height="337" alt="image" src="https://github.com/user-attachments/assets/72c0fde7-5b29-491a-8648-24027c8a0c6b" />

## Action Plan
### Build
Personal precedence-rules spreadsheet: persist Field Authority decisions per agency and surface repeated overrides as automatic defaults, closing the Preference loop gap this workaround is standing in for.

Manual cross-agency knowledge-sharing: build the shared, system crosswalk library, so what agencies are currently doing over email/phone calls happens automatically inside the product.

### Partner
BI tool export/dashboarding (Power BI, Excel): partner to ship a clean, documented export format rather than building dashboarding natively; agencies already have BI tools and licenses, and duplicating that capability inside RyFlow would be effort spent competing with a tool the customer already trusts, not effort spent on the actual product

### Ignore + Monitor
·

## Roadmap Brief
Based on your audit: 3 user-side workarounds discovered.
Decisions: 2 build · 1 partner · 0 ignore · 0 TBD.
Estimated adjacent spend: $50/mo across surveyed users. (most of the cost is on the human hours/labors)
Dominant signal: Capability gap.

Recommended next step: Capability gaps dominate, users want something your product does not do. Strongest near-term move is building one or two of these natively before a competitor does.

Sequence the Build column by frequency × strategic relevance. Confirm Partner candidates with the external tools' partnership teams. Re-run this audit each quarter, workarounds shift fast.

