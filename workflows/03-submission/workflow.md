# Workflow 03: Submission

## Overview

This workflow handles journal selection, cover letter generation, and final submission package assembly. It bridges pre-submission preparation with the actual submission to a journal.

**Primary Agent**: Author Agent
**Supporting Agents**: Production Agent (package assembly)
**Quality Gates**: STOP-04 (submission package approval)

---

## Workflow Diagram

```mermaid
graph TD
    A[Pre-Submission Package from Workflow 02] --> B{Journal Already Selected?}
    B -->|No| C[Journal Selection]
    B -->|Yes| D[Cover Letter Generation]
    C --> C1[Analyze Manuscript Scope & Keywords]
    C1 --> C2[Query Journal Database]
    C2 --> C3[Rank Journals by Fit]
    C3 --> C4[Present Recommendations to Author]
    C4 --> C5{Author Selects Journal}
    C5 --> D
    D --> D1[Gather Journal-Specific Requirements]
    D1 --> D2[Draft Cover Letter]
    D2 --> D3{Author Reviews Cover Letter}
    D3 -->|Revise| D2
    D3 -->|Approve| E[Submission Package Assembly]
    E --> E1[Manuscript File - Final Format]
    E1 --> E2[Cover Letter]
    E2 --> E3[Supplementary Materials]
    E3 --> E4[Figures - High Resolution]
    E4 --> E5[Declarations - COI, Ethics, AI Disclosure]
    E5 --> E6[Author Agreement / Copyright Form]
    E6 --> E7[Suggested Reviewers List]
    E7 --> F[Package Completeness Check]
    F --> G{STOP-04: Author Reviews Complete Package}
    G -->|Missing Items| H[Complete Package]
    H --> F
    G -->|Approved| I[Author Submits via Journal Portal]
    I --> J[Record Submission Details]
    J --> K[Set Review Timeline Expectations → Workflow 04]
```

---

## Steps

### Step 1: Journal Selection
See: `journal-selection.md`

Evidence-based journal matching considering scope, impact, OA policy, turnaround time, and acceptance rate. Invokes `skills/journal-matching.md`.

### Step 2: Cover Letter Generation
See: `cover-letter.md`

Draft a journal-specific cover letter highlighting manuscript significance, relevance to journal scope, and key findings. Invokes `skills/cover-letter-drafting.md`.

### Step 3: Submission Package Assembly
See: `submission-package.md`

Assemble all required files and declarations into a complete submission package. Verify completeness against journal requirements.

### Step 4: Author Approval (STOP-04)

The author must review the complete submission package before submitting. This is a STOP gate — no automated submission.

---

## Sub-Files

| File | Purpose |
|---|---|
| `journal-selection.md` | Evidence-based journal matching |
| `cover-letter.md` | Cover letter generation |
| `submission-package.md` | Submission package assembly and verification |

---

## Skills Used

- `skills/journal-matching.md` — Journal recommendation engine
- `skills/cover-letter-drafting.md` — Cover letter generation
- `skills/ai-disclosure-drafting.md` — If additional disclosure needed for cover letter
