# Workflow 02: Pre-Submission

## Overview

Pre-submission is the quality assurance stage between a complete draft and actual submission. It covers self-review, reference validation, AI disclosure generation, and metadata preparation.

**Primary Agent**: Author Agent
**Supporting Agents**: Integrity Agent (reference validation), Production Agent (metadata)
**Quality Gates**: STOP-02 (citation sign-off), STOP-03 (AI disclosure approval)

---

## Workflow Diagram

```mermaid
graph TD
    A[Complete Draft from Workflow 01] --> B[Self-Review Checklist]
    B --> C{All Checklist Items Pass?}
    C -->|No| D[Address Deficiencies]
    D --> B
    C -->|Yes| E[Reference Validation]
    E --> E1[Extract All References]
    E1 --> E2[Verify Against CrossRef/PubMed/DOI]
    E2 --> E3[Generate Verification Report]
    E3 --> F{STOP-02: Author Reviews Report}
    F -->|Issues Found| G[Resolve Flagged References]
    G --> E2
    F -->|All Clear| H[AI Disclosure Generation]
    H --> H1[Identify Target Publisher]
    H1 --> H2[Check Publisher Policy]
    H2 --> H3[Generate Disclosure Statement]
    H3 --> I{STOP-03: Author Approves Disclosure}
    I -->|Needs Edit| J[Revise Disclosure]
    J --> I
    I -->|Approved| K[Metadata Preparation]
    K --> K1[Author ORCID Verification]
    K1 --> K2[CRediT Role Assignment]
    K2 --> K3[JATS-XML Metadata]
    K3 --> K4[Funding & COI Statements]
    K4 --> L{All Metadata Complete?}
    L -->|No| M[Complete Missing Metadata]
    M --> K
    L -->|Yes| N[Pre-Submission Package Ready → Workflow 03]
```

---

## Steps

### Step 1: Self-Review Checklist
See: `self-review-checklist.md`

Comprehensive pre-submission checklist covering content, formatting, ethics, and compliance.

### Step 2: Reference Validation
See: `reference-validation.md`

Full citation verification using CrossRef, PubMed, and DOI resolution. This is a STOP gate (STOP-02) — all flagged references must be resolved before proceeding.

### Step 3: AI Disclosure Generation
See: `ai-disclosure-generator.md`

Generate a publisher-specific AI disclosure statement based on the actual AI use during manuscript preparation. This is a STOP gate (STOP-03) — the author must review and approve the disclosure.

### Step 4: Metadata Preparation
See: `metadata-preparation.md`

Prepare all required metadata: ORCID iDs, CRediT author contributions, JATS-XML metadata, funding statements, COI declarations, and data availability statements.

---

## Sub-Files

| File | Purpose |
|---|---|
| `self-review-checklist.md` | Comprehensive pre-submission quality checklist |
| `reference-validation.md` | Citation verification procedures |
| `ai-disclosure-generator.md` | Publisher-specific AI disclosure generation |
| `metadata-preparation.md` | JATS-XML, ORCID, CRediT, and other metadata |

---

## Skills Used

- `skills/citation-verification.md` — Full reference verification
- `skills/ai-disclosure-drafting.md` — Publisher-specific disclosure
- `skills/credit-taxonomy.md` — CRediT role assignment
- `skills/jats-xml-conversion.md` — Metadata structuring
- `skills/readability-analysis.md` — Final readability check
