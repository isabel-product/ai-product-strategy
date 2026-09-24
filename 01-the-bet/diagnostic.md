# Three-Axis Vulnerability Diagnostic

## Product
<!-- Name the product you're diagnosing. Real product at your company — not a hypothetical. --> RyFlow

**Product:** RyFlow is an AI-driven data-integration and quality layer that reconciles client and encounter records across a Ryan White program's clinical, case management, and reporting systems so staff can stop manually de-duplicating data and trust what they submit for required federal reporting. RyFlow produces clean, de-duplicated, cross-validated data ready for RSR (Ryan White Services Report) and ADR (Annual Data Report) submission. The core pain it targets: program staff currently do manual de-duplication and re-key the same client/encounter data into multiple systems, which erodes data quality and burns staff time every reporting cycle.
**Your Role:** Director of Product

---

## Scores

### Contextual Moat — 3/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?* 3

**Score rationale:** Once a program maps its field-level crosswalks (Epic ↔ CAREWare ↔ case management ↔ lab feed ↔ legacy system) and trains staff on the reconciliation workflow, switching cost is high — re-mapping dozens of fields across 4-6 systems per client agency is not an easy task.

**Named attacker (from partner challenge):** A competing integration vendor who wins the initial mapping engagement before RyFlow

---

### Data Advantage — 2/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?* 2

**Score rationale:** The product sees every field-level mismatch and manual correction a program makes, which is a correction history that could compound into a reusable crosswalk library (e.g., "this is how Epic's race/ethnicity codes map to RSR categories" across many agencies), which would be a compounding asset with each new integration. But today, it would start as a one-agency-at-a-time mapping tool with no stated network effect across agencies. The advantage is latent, not built.

**Named attacker (from partner challenge):** HRSA's CAREWare  if they extend CAREWare's native import/export tooling; also Epic's interoperability layer (App Orchard / Epic on FHIR) solving mapping generically

---

### Platform Exposure — 3/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?* 3

**Score rationale: If CAREWare (free, HRSA-funded, near-universal in Ryan White programs) ships a native "import wizard" with better field mapping and de-dup, or if Epic's Bridges/FHIR interfaces mature enough to push clean data downstream automatically, a chunk of RyFlow's value evaporates. The counter-risk is lower than a consumer SaaS category because CAREWare is a slow-moving, grant-funded, feature-conservative product — but it is the single most obvious platform threat here.**

**Named attacker (from partner challenge):** CAREWare the currently free Ryan White reporting platform

---

## Top Vulnerability
<!-- One line: what's the single biggest strategic risk? -->  Data Advantage is the weakest axis — RyFlow's real defensibility depends on turning single-agency field mappings into a cross-agency crosswalk library over time.


## Confidence Level
<!-- H / M / L — how confident are you in this bet after the diagnostic? --> M: The pain point is specific, real, and under-served (Ryan White programs are a niche too small for larger integration vendor to prioritize, but the manual burden is well-documented in the domain). The main open risk is whether the business model is a scalable product or a services-heavy integration practice.

