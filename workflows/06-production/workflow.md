# Workflow 06: Production

## Overview

Post-acceptance production workflow covering copyediting, readability analysis, typesetting QA, and metadata validation. Ensures the final published version is polished, accessible, and accurately indexed.

**Primary Agent**: Production Agent
**Supporting Agents**: Author Agent (proof review)
**Quality Gates**: STOP-09 (final publication approval)

---

## Workflow Diagram

```mermaid
graph TD
    A[Accepted Manuscript] --> B[Copyediting]
    B --> B1[Grammar & Style Check]
    B1 --> B2[Readability Analysis]
    B2 --> B3[Consistency Check]
    B3 --> B4[Reference Format Verification]
    B4 --> C{Copyediting Complete?}
    C -->|Issues Remain| D[Address Issues]
    D --> B
    C -->|Complete| E[Typesetting]
    E --> E1[Layout Formatting]
    E1 --> E2[Figure/Table Placement]
    E2 --> E3[Header/Footer/Pagination]
    E3 --> F[Typesetting QA]
    F --> F1[Visual Inspection]
    F1 --> F2[Text Integrity Check]
    F2 --> F3[Figure Quality Check]
    F3 --> F4[Cross-Reference Verification]
    F4 --> G{QA Passed?}
    G -->|No| H[Fix Issues]
    H --> F
    G -->|Yes| I[Metadata Validation]
    I --> I1[DOI Assignment/Verification]
    I1 --> I2[CrossRef Metadata Deposit]
    I2 --> I3[JATS-XML Validation]
    I3 --> I4[Author/Affiliation Check]
    I4 --> J{Metadata Valid?}
    J -->|No| K[Fix Metadata]
    K --> I
    J -->|Yes| L[Author Proofs]
    L --> M{STOP-09: Author Reviews Proofs}
    M -->|Corrections Needed| N[Author Corrections]
    N --> E
    M -->|Approved| O[Publish]
    O --> P[→ Workflow 07: Post-Publication]
```

---

## Steps

### Step 1: Copyediting
See: `copyediting.md`

AI-assisted copyediting with readability analysis. Covers grammar, style, consistency, and accessibility while preserving technical meaning.

### Step 2: Typesetting QA
See: `typesetting-qa.md`

Quality assurance for the typeset version — layout, figures, tables, cross-references, and pagination.

### Step 3: Metadata Validation
See: `metadata-validation.md`

Verify all metadata for accurate indexing: DOI, CrossRef deposit, JATS-XML, author/affiliation data, funding information, and keywords.

### Step 4: Author Proofs (STOP-09)

The author must review and approve final proofs before publication. This is the last chance to catch errors.

---

## Sub-Files

| File | Purpose |
|---|---|
| `copyediting.md` | AI-assisted copyediting with readability analysis |
| `typesetting-qa.md` | Layout and typesetting quality assurance |
| `metadata-validation.md` | DOI, CrossRef, JATS-XML, and metadata verification |

---

## Skills Used

- `skills/readability-analysis.md` — Flesch-Kincaid, SMOG, Gunning Fog scoring
- `skills/jats-xml-conversion.md` — JATS-XML generation and validation
- `skills/citation-verification.md` — Final reference verification
