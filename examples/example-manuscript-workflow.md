# Example: Author Manuscript Workflow

## Scenario

Dr. Dylan Mordaunt, a health economics researcher at Flinders University, is preparing a manuscript on the cost-effectiveness of telehealth interventions in rural Australian settings. He wants AI assistance from initial draft through submission to Health Economics (Wiley).

---

## Workflow Trace

### Stage 1: Manuscript Preparation (Workflow 01)

**User**: "Help me prepare my manuscript on telehealth cost-effectiveness for submission to Health Economics."

**Orchestrator Agent** → Routes to **Author Agent**

**Author Agent Actions**:

1. **Reads rules**: `rules/ai-ethics.md`, `rules/citation-integrity.md`
2. **Checks journal requirements**: Loads `config/journal-requirements.yaml` → Health Economics entry
   - Word limit: 8,000
   - Abstract: 200 words, unstructured
   - Reference style: Harvard (author-year)
   - Double-spaced

3. **Literature Review** (`workflows/01-manuscript-preparation/literature-review.md`):
   - PubMed search: `("telehealth" OR "telemedicine") AND ("cost-effectiveness" OR "economic evaluation") AND "rural"`
   - Results: 187 papers identified, 34 directly relevant after screening
   - **Citation Verification** (`skills/citation-verification.md`): All 34 references verified against CrossRef
     - 32 VERIFIED ✅
     - 2 PARTIALLY_VERIFIED (corrected: wrong volume numbers) ✅

4. **Drafting** (`workflows/01-manuscript-preparation/drafting.md`):
   - Author provides: study design, model structure, data sources, results
   - AI assists with: Introduction structure, Methods standardized language, Discussion organization
   - AI does NOT generate: data, statistics, results interpretation
   - **AI Assistance Log**: Records that Claude assisted with language editing in Introduction, Methods (standard descriptions), and Discussion sections

5. **STOP-01: Author Reviews Draft** 🛑
   ```
   AWAITING AUTHOR APPROVAL
   - Draft complete: 5,200 words (within 8,000 limit)
   - All 34 references verified
   - AI assistance logged for disclosure
   Please review the complete draft and approve or request changes.
   ```
   **Author**: Reviews, makes edits, approves. → STOP-01 CLEARED ✅

6. **Formatting Compliance** (`workflows/01-manuscript-preparation/formatting-compliance.md`):
   - Word count: 5,200 ✅ (limit 8,000)
   - Abstract: 185 words ✅ (limit 200)
   - Reference style: Harvard ✅
   - Structure: IMRAD ✅
   - WARN-06: 3 references from 2015 flagged as potentially outdated → Author reviewed, 2 remain relevant, 1 updated

### Stage 2: Pre-Submission (Workflow 02)

**Author Agent Actions**:

1. **Self-Review Checklist** (`workflows/02-pre-submission/self-review-checklist.md`):
   - 42/44 items checked ✅
   - Missing: Data availability statement, AI disclosure statement
   - Action: Added data availability statement. AI disclosure to be generated.

2. **Reference Validation** (`workflows/02-pre-submission/reference-validation.md`):
   - Full verification of 34 references against CrossRef
   - Results: 34/34 VERIFIED ✅
   - **STOP-02** 🛑: Author signs off on citation verification report → CLEARED ✅

3. **AI Disclosure Generation** (`workflows/02-pre-submission/ai-disclosure-generator.md`):
   - Target: Wiley (Health Economics)
   - Template: `templates/ai-disclosure-wiley.md`
   - Generated disclosure:

   > "The authors disclose the use of Claude 3.5 Sonnet (Anthropic, January 2026) during the preparation of this manuscript. The tool was used for language editing in the Introduction, Methods, and Discussion sections, and for literature search assistance. All identified references were independently verified against CrossRef. The tool was not used for data analysis, model construction, or results interpretation. All AI-assisted content was reviewed, verified, and edited by all authors, who take full responsibility for all content in this publication."

   - **STOP-03** 🛑: Author reviews and approves disclosure → CLEARED ✅

4. **Metadata Preparation** (`workflows/02-pre-submission/metadata-preparation.md`):
   - ORCID iDs: Verified for all 3 authors ✅
   - CRediT roles: Assigned using `skills/credit-taxonomy.md`
     - DAM: Conceptualization, Methodology, Funding acquisition, Supervision, Writing – original draft, Writing – review & editing
     - Co-author 2: Formal analysis, Software, Visualization, Writing – review & editing
     - Co-author 3: Data curation, Investigation, Validation, Writing – review & editing
   - Funding: NHMRC grant number XXXXXXX
   - COI: No conflicts declared
   - Data availability: "Available from corresponding author upon reasonable request"

### Stage 3: Submission (Workflow 03)

**Author Agent Actions**:

1. **Journal Selection** (`skills/journal-matching.md`):
   - Already selected: Health Economics (Wiley)
   - Fit score: 92% — confirmed as appropriate target
   - Backup plan: Value in Health → BMC Health Services Research

2. **Cover Letter** (`skills/cover-letter-drafting.md`):
   - Template: `templates/cover-letter-template.md`
   - Addressed to the Editor-in-Chief
   - Highlights: novel decision-analytic model for rural Australian context, significant cost savings, policy relevance
   - Includes 3 suggested reviewers (verified no COI)
   - Author reviews and approves ✅

3. **Submission Package** (`workflows/03-submission/submission-package.md`):
   ```
   SUBMISSION PACKAGE SUMMARY
   ✅ Manuscript (5,200 words, .docx)
   ✅ Cover letter (.pdf)
   ✅ Figure 1: Decision tree model (600 DPI TIFF)
   ✅ Figure 2: Cost-effectiveness plane (600 DPI TIFF)
   ✅ Figure 3: Tornado diagram (600 DPI TIFF)
   ✅ Table S1: Model parameters (supplementary, .docx)
   ✅ Table S2: Sensitivity analysis results (supplementary, .docx)
   ✅ All declarations complete (COI, funding, ethics, AI disclosure, CRediT)
   ✅ Suggested reviewers: 3 provided
   ```

   - **STOP-04** 🛑: Author reviews complete package
   ```
   AWAITING AUTHOR APPROVAL FOR SUBMISSION
   All files verified. All declarations complete.
   You will need to upload these to the Health Economics ScholarOne portal.
   ```
   → Author approves → CLEARED ✅
   → Author submits via ScholarOne (manual action)

4. **Post-Submission Record**:
   ```yaml
   submission_record:
     journal: "Health Economics"
     publisher: "Wiley"
     manuscript_id: "HEC-2026-0042"
     submission_date: "2026-01-20"
     expected_initial_decision: "2026-03-17"
     status: "Under Review"
   ```

---

## Audit Trail Summary

| Timestamp | Agent | Action | Gate |
|---|---|---|---|
| 2026-01-10 09:00 | Orchestrator | Pipeline initiated | — |
| 2026-01-10 09:15 | Author Agent | Literature search | — |
| 2026-01-10 11:00 | Author Agent | Citation verification (34 refs) | — |
| 2026-01-12 14:00 | Author Agent | Draft complete | STOP-01 ⏳ |
| 2026-01-12 16:00 | Human | Draft approved | STOP-01 ✅ |
| 2026-01-13 10:00 | Author Agent | Formatting compliance check | WARN-06 |
| 2026-01-14 09:00 | Author Agent | Self-review checklist | — |
| 2026-01-14 11:00 | Author Agent | Full reference validation | STOP-02 ⏳ |
| 2026-01-14 11:30 | Human | Citations signed off | STOP-02 ✅ |
| 2026-01-14 12:00 | Author Agent | AI disclosure generated | STOP-03 ⏳ |
| 2026-01-14 12:15 | Human | Disclosure approved | STOP-03 ✅ |
| 2026-01-15 10:00 | Author Agent | Metadata preparation | — |
| 2026-01-16 09:00 | Author Agent | Cover letter drafted | — |
| 2026-01-16 14:00 | Author Agent | Submission package assembled | STOP-04 ⏳ |
| 2026-01-16 15:00 | Human | Package approved | STOP-04 ✅ |
| 2026-01-20 10:00 | Human | Submitted via ScholarOne | — |
