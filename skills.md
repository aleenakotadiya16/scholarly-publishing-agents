# skills.md — Master Skill Index

This document indexes all 12 skills in the scholarly publishing workflow system. Each skill is a reusable, composable procedure that can be invoked by agents or directly by users.

For full skill definitions, see the individual files in `skills/`.

---

## Skill Overview

| # | Skill | Description | Primary Agent(s) |
|---|---|---|---|
| 1 | [Citation Verification](#1-citation-verification) | Verify references against CrossRef/PubMed/DOI | Author, Integrity |
| 2 | [Readability Analysis](#2-readability-analysis) | Score text using Flesch-Kincaid, SMOG, Gunning Fog | Production, Author |
| 3 | [Statistical Review](#3-statistical-review) | Check statistical methods and reporting completeness | Reviewer, Integrity |
| 4 | [Plagiarism Screening](#4-plagiarism-screening) | Detect text overlap and originality concerns | Integrity |
| 5 | [Image Integrity](#5-image-integrity) | Detect duplicated or manipulated images | Integrity |
| 6 | [JATS-XML Conversion](#6-jats-xml-conversion) | Convert manuscripts to JATS-XML format | Production |
| 7 | [Journal Matching](#7-journal-matching) | Match manuscripts to suitable journals | Author |
| 8 | [AI Disclosure Drafting](#8-ai-disclosure-drafting) | Generate publisher-specific AI use statements | Author |
| 9 | [CRediT Taxonomy](#9-credit-taxonomy) | Assign contributor roles per CRediT standard | Author |
| 10 | [PRISMA Compliance](#10-prisma-compliance) | Check systematic review reporting compliance | Author, Reviewer |
| 11 | [Cover Letter Drafting](#11-cover-letter-drafting) | Generate evidence-based cover letters | Author |
| 12 | [Response Letter Drafting](#12-response-letter-drafting) | Draft point-by-point reviewer responses | Author |

---

## Skill Details

### 1. Citation Verification

**File**: `skills/citation-verification.md`

**Description**: Verifies that every reference in a manuscript exists and is accurately cited by checking against CrossRef, PubMed, and DOI registries. Detects hallucinated citations, blended references, fabricated authors, and nonexistent journals.

**Inputs**: Reference list (structured or unstructured), manuscript text with in-text citations

**Outputs**: Verification report with status per reference (verified / unverified / suspicious / not found), confidence scores, suggested corrections

**Cross-references**:
- Rules: `rules/citation-integrity.md`
- Workflows: `workflows/02-pre-submission/reference-validation.md`
- Agents: Author Agent, Integrity Agent

---

### 2. Readability Analysis

**File**: `skills/readability-analysis.md`

**Description**: Analyzes text readability using established metrics — Flesch-Kincaid Grade Level, SMOG Index, Gunning Fog Index, Coleman-Liau Index, and Automated Readability Index. Provides audience-appropriate recommendations.

**Inputs**: Text content (full manuscript or section), target audience (general public, clinicians, researchers), target journal

**Outputs**: Readability scores, audience appropriateness assessment, specific improvement suggestions, sentence-level flagging of overly complex passages

**Cross-references**:
- Skills: Uses `textstat` MCP server when available
- Workflows: `workflows/06-production/copyediting.md`
- Agents: Production Agent, Author Agent

---

### 3. Statistical Review

**File**: `skills/statistical-review.md`

**Description**: Reviews statistical methods and reporting for completeness and appropriateness. Checks for common errors (e.g., misuse of parametric tests on non-normal data), missing effect sizes, unreported confidence intervals, and suspicious statistical patterns.

**Inputs**: Manuscript methods and results sections, supplementary data if available

**Outputs**: Statistical reporting completeness score, list of missing elements, appropriateness assessment, flags for suspicious patterns (GRIM/SPRITE test results)

**Cross-references**:
- Workflows: `workflows/04-peer-review/integrity-screening.md`
- Agents: Reviewer Agent, Integrity Agent
- Standards: SAMPL guidelines, EQUATOR Network reporting guidelines

---

### 4. Plagiarism Screening

**File**: `skills/plagiarism-screening.md`

**Description**: Screens text for potential plagiarism, text recycling, and excessive similarity to published works. Identifies direct copying, close paraphrasing, and structural plagiarism.

**Inputs**: Manuscript text, optional reference corpus

**Outputs**: Similarity report with flagged passages, source identification where possible, recommended actions (rewrite, cite, accept as common knowledge)

**Cross-references**:
- Rules: `rules/ai-ethics.md`
- Workflows: `workflows/04-peer-review/integrity-screening.md`
- Agents: Integrity Agent

---

### 5. Image Integrity

**File**: `skills/image-integrity.md`

**Description**: Detects potential image manipulation, duplication, and splicing in manuscript figures. Uses perceptual hashing, pixel-level analysis, and metadata examination.

**Inputs**: Manuscript figures (images), figure legends, manuscript text referencing figures

**Outputs**: Integrity report per figure (clean / suspicious / flagged), specific concerns (duplication, splicing, enhancement), recommended actions

**Cross-references**:
- Workflows: `workflows/04-peer-review/integrity-screening.md`
- Agents: Integrity Agent
- Context: Hindawi/Wiley paper mill detection methods

---

### 6. JATS-XML Conversion

**File**: `skills/jats-xml-conversion.md`

**Description**: Converts manuscript content into JATS-XML (Journal Article Tag Suite) format for submission and archiving. Supports JATS 1.3 Blue (publishing), Green (archiving), and Orange (authoring) tag sets.

**Inputs**: Manuscript content (structured), metadata (authors, affiliations, funding), reference list

**Outputs**: Valid JATS-XML document, validation report, conversion warnings

**Cross-references**:
- Workflows: `workflows/02-pre-submission/metadata-preparation.md`, `workflows/06-production/metadata-validation.md`
- Agents: Production Agent
- Standards: JATS 1.3 (NISO Z39.96-2019)

---

### 7. Journal Matching

**File**: `skills/journal-matching.md`

**Description**: Matches a manuscript to suitable target journals based on scope, impact factor, open access policy, turnaround time, acceptance rate, and audience. Considers the author's career stage and goals.

**Inputs**: Manuscript abstract, keywords, discipline, author preferences (OA, speed, prestige), previous submission history

**Outputs**: Ranked list of recommended journals with rationale, fit scores, key requirements per journal, potential concerns

**Cross-references**:
- Config: `config/journal-requirements.yaml`
- Workflows: `workflows/03-submission/journal-selection.md`
- Agents: Author Agent

---

### 8. AI Disclosure Drafting

**File**: `skills/ai-disclosure-drafting.md`

**Description**: Generates publisher-specific AI use disclosure statements based on how AI was used in the manuscript preparation process. Ensures compliance with current publisher policies.

**Inputs**: Publisher/journal target, description of AI tools used, description of how AI was used (drafting, editing, analysis, literature search, etc.)

**Outputs**: Publisher-compliant disclosure statement, placement recommendation (Methods, Acknowledgements, separate declaration), compliance checklist

**Cross-references**:
- Rules: `rules/disclosure-compliance.md`
- Config: `config/publisher-policies.yaml`
- Templates: `templates/ai-disclosure-*.md`
- Workflows: `workflows/02-pre-submission/ai-disclosure-generator.md`
- Agents: Author Agent

---

### 9. CRediT Taxonomy

**File**: `skills/credit-taxonomy.md`

**Description**: Assists in assigning CRediT (Contributor Roles Taxonomy) roles to manuscript authors. Maps author contributions to the 14 standardized CRediT roles.

**Inputs**: Author list, description of each author's contributions

**Outputs**: CRediT role assignments per author, formatted contribution statement, validation flags (e.g., role assigned to no one, author with no roles)

**Cross-references**:
- Workflows: `workflows/02-pre-submission/metadata-preparation.md`
- Agents: Author Agent
- Standards: CRediT (NISO Z39.104), ICMJE authorship criteria

---

### 10. PRISMA Compliance

**File**: `skills/prisma-compliance.md`

**Description**: Checks systematic review manuscripts against the PRISMA 2020 checklist (or PRISMA-ScR for scoping reviews). Identifies missing reporting items and provides recommendations.

**Inputs**: Systematic review manuscript, review protocol (if available), PRISMA variant (PRISMA 2020, PRISMA-ScR, PRISMA-P)

**Outputs**: Compliance checklist with status per item (reported / partially reported / not reported / not applicable), overall compliance score, specific recommendations for missing items

**Cross-references**:
- Workflows: `workflows/01-manuscript-preparation/formatting-compliance.md`
- Agents: Author Agent, Reviewer Agent
- Standards: PRISMA 2020, PRISMA-ScR, EQUATOR Network

---

### 11. Cover Letter Drafting

**File**: `skills/cover-letter-drafting.md`

**Description**: Generates evidence-based cover letters tailored to specific journals. Highlights manuscript significance, relevance to journal scope, and key findings. Avoids generic language.

**Inputs**: Manuscript abstract, target journal, key findings, author information, any special considerations (e.g., invited submission, special issue)

**Outputs**: Draft cover letter, journal-specific customization notes, checklist of required cover letter elements for the target journal

**Cross-references**:
- Templates: `templates/cover-letter-template.md`
- Workflows: `workflows/03-submission/cover-letter.md`
- Agents: Author Agent

---

### 12. Response Letter Drafting

**File**: `skills/response-letter-drafting.md`

**Description**: Assists in drafting point-by-point response letters to reviewer and editor comments. Structures responses clearly, ensures all points are addressed, and maintains professional tone.

**Inputs**: Reviewer comments (all reviewers), editor decision letter, revised manuscript (with tracked changes), author's notes on how each point was addressed

**Outputs**: Formatted response letter with point-by-point responses, change location references, summary of major revisions, checklist confirming all points addressed

**Cross-references**:
- Templates: `templates/response-to-reviewers-template.md`
- Workflows: `workflows/05-revision/response-to-reviewers.md`
- Agents: Author Agent

---

## Skill Dependency Map

```
                    ┌──────────────┐
                    │   Citation   │
            ┌───────│ Verification │───────┐
            │       └──────────────┘       │
            ▼                              ▼
   ┌──────────────┐              ┌──────────────┐
   │   PRISMA     │              │  Statistical │
   │  Compliance  │              │   Review     │
   └──────────────┘              └──────────────┘
            │                              │
            │       ┌──────────────┐       │
            └──────►│  Plagiarism  │◄──────┘
                    │  Screening   │
                    └──────────────┘
                           │
                    ┌──────▼───────┐
                    │    Image     │
                    │  Integrity   │
                    └──────────────┘

   ┌──────────────┐  ┌──────────────┐  ┌──────────────┐
   │   Journal    │  │ AI Disclosure│  │   CRediT     │
   │   Matching   │──│   Drafting   │──│  Taxonomy    │
   └──────────────┘  └──────────────┘  └──────────────┘
         │                                     │
         ▼                                     ▼
   ┌──────────────┐              ┌──────────────┐
   │ Cover Letter │              │  JATS-XML    │
   │   Drafting   │              │  Conversion  │
   └──────────────┘              └──────────────┘
                                       │
                                       ▼
                              ┌──────────────┐
                              │ Readability  │
                              │  Analysis    │
                              └──────────────┘
                                       │
                                       ▼
                              ┌──────────────┐
                              │  Response    │
                              │   Letter     │
                              └──────────────┘
```
