# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 3/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 2/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 2/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 3/5 |

### Correction Loop - 3/5
**What you capture today:** When a reviewer accepts or overrides a suggested mapping, the product logs that decision and uses it to change what it suggests in the future — both for that same field in that system, and for related fields in the same category.
**How it compounds:** Because the correction directly changes future suggestion confidence rather than just sitting in a record, the next mapping screen a user sees is different because of the correction they made.

### Preference Loop - 1/5
**What you capture today:** The model does not currently capture induvial preferences. Nothing yet. Field Authority precedence picks (which system is trusted per field) are stored per agency, but the product doesn't track a reviewer's repeated behavior or turn it into an automatic default.
**How it compounds:** N/A, no mechanism exists today.

### Domain Context Loop - 2/5
**What you capture today:** The model does not currently capture loops that will cross loops. It may support other domains if other domains also use similar fields as the Ryan White space (gender, age, DOB, and other demographics will be transferrable; however other data like HIV labs will not transfer to other domains due to its lack of relevance)
**How it compounds:**N/A, this only works within a single domain, other than demographics. 

### Network Loop - 3/5
**What you capture today:** Every agency's confirmed field mappings write into a shared library keyed by system type (CAREWare, Epic, Cerner, eHARS, case management). When agency #2 onboards, its Epic mapping screen already shows high-confidence defaults pulled from every prior agency's confirmed Epic mappings — before agency #2 has corrected anything itself.
**How it compounds:**More agencies using the product means more confirmed mappings feeding each system-type library, which means faster, higher-confidence onboarding for the next agency, which brings in more agencies. Each new customer makes the product measurably better for every future customer — the core definition of a network effect.

**Total Flywheel Score: 9/20**
**Weakest Loop:** Preference Loop
**Fix for weakest loop:** Currently, we are not considering tracking preference of field authority. However preference of which field should be the trusted source for the reporting layer (RSR/ADR reports) can be tracked and kept in the product's memory. The fix would be to save agency-specific decisions in a database, including tracking which overrides a given agency's staff make repeatedly — if the same reviewer consistently picks CAREWare over Case Management for insurance status, surface that as the default the next time a similar conflict appears, instead of asking them to make the same decision again and again. 

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** HRSA/HAB's own CAREWare product team
**Vector:** Ships a native multi-source import wizard with basic de-dup, built into a tool nearly every Ryan White grantee already uses for free
**Time-to-threat:**12-18 months (CAREWare is grant-funded and feature-conservative, but this is the single most obvious platform-owned wedge)
**% of value at risk:**~40%

### 2. Vertical Competitor
**Attacker:**Triyoung (CAREWare implementation/consulting partner)
**Vector:** uilds a narrower, deeper de-dup tool for one state or consortium they already serve, using relationships they already have
**Time-to-threat:** 6-9 months (low technical barrier, no cold-start sales problem)
**% of value at risk:** ~25%

### 3. Adjacent Expansion
**Attacker:** Palantir
**Vector:** Wins a broader federal health-data consolidation contract (their existing HHS/VA-style playbook) and adds Ryan White RSR/ADR reconciliation as an extension of that mandate — winning through an existing federal relationship and distribution, not by selling directly to individual grantees
**Time-to-threat:** 9-12 months (contingent on when/whether such a federal contract materializes, not on their technical readiness — they could build the capability quickly once positioned)
**% of value at risk:** ~35%

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Palantir
**Attack vector (target the weakest loop):** Palantir doesn't need to out-build the crosswalk library; they attack by winning the bigger federal relationship and folding in personalization RyFlow hasn't gotten to yet.
**Weeks 1-4 - what they ship:** Palantir pitches HRSA/HAB directly on a federal Ryan White data platform — not a per-agency tool, but a centralized ontology across every grantee's CAREWare, Epic, and case management data. 
**Weeks 5-8 - how they poach users:** HRSA leadership, not individual agencies, becomes the target — a single federal contract conversation reaches every grantee at once, bypassing agency-by-agency sales entirely. 
**Weeks 9-12 - why users don't come back:** Once a federal contract is signed, and the agencies are tied to another product, they will have to find other ways to fund third party tools, and may choose not to come back even if RyFlow's shared crosswalk library is  stronger. 
**Your defense:** Make RyFlow's value depend on accumulated, agency-specific state that a generic platform can't replicate by copying a feature. Keep building out the Network and Domain Context loops so that every agency's resolved conflicts, confirmed crosswalks, and precedence decisions accumulate into a growing dataset that makes the product measurably better for agencies and programs over time. Pair that with genuine workflow depth: RyFlow shouldn't just suggest a mapping once, it should own the ongoing reconciliation loop (new client records, updated lab results, changed eligibility status) so that ripping it out means losing a live process, not swapping one static tool for another. A platform can copy "suggest a field mapping" in a quarter. It's much harder to copy three years of an agency's actual resolved data-quality decisions embedded in a system that keeps running against real, current data.
