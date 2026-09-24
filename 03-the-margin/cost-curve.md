# Cost Curve & Pricing Strategy

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) |$.25 |~20-50 field-mapping suggestion calls/month at a classification-task rate; heaviest during onboarding, then mostly idle until a source system's schema changes |
| Inference (cascading/triage) |$0.03 |A lightweight model handles the bulk of routine field matches; only low-confidence cases would ever need to escalate to a stronger model |
| Infrastructure | $110 |Hosting, integration connections (Epic/CAREWare/case management endpoints), and de-dup matching compute (Splink-style, not AI-driven, but real compute cost that scales with client record volume) |
| Data/storage |$35 |Client records, mapping configs, audit logs — grows with agency size, not with AI usage |
| Human-in-the-loop |NA |Happens on the customer's side-- agency staff reviewing suggestions, not a cost RyFlow absorbs |
| **Total AI COGS** | $145.28 |Cost is mostly driven by infrastructure |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model:** A small, cheap classification model handles the default case — matching a source field name/sample values to one of ~20-30 canonical RSR/ADR fields. This is not a task requiring frontier intelligence.
**Frontier model:**Reserved only for low-confidence matches the triage model can't resolve cleanly — e.g., ambiguous or unusually-named fields where a stronger model's broader pattern recognition might close the gap before falling back to "map by hand."
**Routing rule:**If triage-model confidence < 70%, escalate to the frontier model once; if still below threshold, surface as "no match — map by hand" rather than looping further.
**Expected cascade ratio:**~90-95% handled by the triage model, ~5-10% escalated to frontier — most field names are recognizable enough (patient.dob, client.race) that they don't need heavier reasoning.

## Pricing Model

**Current pricing:** None yet, no live product. For modeling purposes, the reference point used elsewhere in this doc is a flat $400/month per agency, which yields 63.7% gross margin at a mid-size agency's $145.28 real cost basis.
**Proposed AI pricing:** Not priced as a separate line item. AI inference (field-mapping suggestions) costs under $0.30/agency/month even at the higher end of usage — negligible relative to the $145.28 total cost basis, which is dominated by infrastructure and storage, not AI. Breaking AI out as its own priced line would add complexity without capturing meaningful additional value; it's bundled into the base fee as part of the core platform.
**Model:** Hybrid to include a base fee per agency (covering integration setup and maintenance) plus usage (number of reconciled records). A base fee per agency ($400/month, covering integration setup and maintenance) plus usage (number of client records reconciled per cycle, at $0.15/record). At a mid-size agency (800 records/month), this lands at ~$520/month and lifts gross margin from 63.7% (flat-fee baseline) to 72.1%, since the metered component scales revenue with agency size the same way real infrastructure and storage cost already does.

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | Minimal as the AI cost is not a fragile line as compared to other costs |No pricing response needed at current scale. Revisit only if a future AI-heavy feature (e.g., something embeddings-driven at high volume) meaningfully changes the cost base this test is run against. |
| Heaviest segment doubles |Heavier usage already generates proportionally more revenue, not just more cost. The real risk isn't record volume doubling — it's conflict rate doubling (agencies whose systems disagree far more than the 60-70% baseline), since that drives more Reconciliation Queue load and more support burden without necessarily showing up in the primary meter if conflicts aren't priced as their own line. | Add the secondary metered line-- a smaller per-conflict-resolved rate on top of per-record-checked, so that a spike in conflict rate — not just record count — is also captured in revenue, not absorbed as a hidden cost.|
| Model provider raises prices 50% | Still not a big impact as the model costs are low compared to other costs| No pricing response needed|

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):** A flat $400/month subscription per agency, regardless of size or number of client records. A 200-client program and a 3,000-client program pay identically — against a $145.28 real cost basis for a mid-size agency, that flat fee yields gross margin of just 63.7%, with a small CBO likely paying the same $400 while costing far less to serve, and a large consortium paying the same $400 while costing meaningfully more.
**After (AI-enabled):** $400/month base + $0.15 per client record reconciled per cycle. A mid-size agency (800 records) lands at ~$520/month; a large consortium (3,000 records) lands at ~$850/month — pricing now scales with the actual value delivered, not just platform access.
**Net margin shift:** Earning more revenue due to the metered addition which scales revenue with the size of clients. At the mid-size agency's $145.28 cost basis, moving from flat $400 to metered $520 lifts gross margin from 63.7% to 72.1% — a real improvement, not just more total revenue. The metered structure captures value proportional to agency size, so larger agencies stop being under-charged relative to what they actually cost to serve.
