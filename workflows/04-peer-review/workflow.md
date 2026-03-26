# Workflow 04: Peer Review

## Overview

This workflow supports all stakeholders in the peer review process: reviewers conducting reviews, editors triaging manuscripts and matching reviewers, and integrity screening for paper mill detection and data verification.

**Primary Agents**: Reviewer Agent, Editor Agent, Integrity Agent
**Quality Gates**: STOP-05 (review submission), STOP-06 (editorial decision), STOP-07 (integrity escalation)

---

## Workflow Diagram

```mermaid
graph TD
    A[Manuscript Submitted] --> B[Editor Receives Manuscript]
    B --> C[Editor Triage]
    C --> C1[Scope Check]
    C1 --> C2[Quality Screen]
    C2 --> C3[Integrity Screen]
    C3 --> D{Triage Decision}
    D -->|Desk Reject| E[STOP-06: Editor Decision - Reject]
    D -->|Send to Review| F[Reviewer Matching]
    D -->|Integrity Concern| G[STOP-07: Integrity Escalation]
    F --> F1[Identify Candidate Reviewers]
    F1 --> F2[Check Conflicts of Interest]
    F2 --> F3[Invite Reviewers]
    F3 --> H{Reviewers Accept?}
    H -->|No| F1
    H -->|Yes| I[Review Period]
    I --> I1[Reviewer Agent Assists Review]
    I1 --> I2[Structured Assessment]
    I2 --> I3[Statistical Checks]
    I3 --> I4[Citation Verification]
    I4 --> I5[Integrity Screening]
    I5 --> J[STOP-05: Reviewer Approves Review]
    J --> K[Reviews Collected]
    K --> L[Editor Reviews All Reports]
    L --> M[Decision Support]
    M --> N{STOP-06: Editorial Decision}
    N -->|Accept| O[→ Workflow 06: Production]
    N -->|Minor Revisions| P[→ Workflow 05: Revision]
    N -->|Major Revisions| P
    N -->|Reject| Q[Decision Letter to Author]
    N -->|Reject & Resubmit| Q
```

---

## Steps

### Step 1: Editor Triage
See: `editor-triage.md`

Initial manuscript screening for scope alignment, basic quality, and integrity red flags. Can result in desk rejection (saves reviewer time) or progression to peer review.

### Step 2: Integrity Screening
See: `integrity-screening.md`

Dedicated integrity checks: paper mill detection (tortured phrases, suspicious metadata), image forensics, statistical consistency, and citation network analysis.

### Step 3: Reviewer Matching
See: `reviewer-matching.md`

Identify and recommend reviewers based on expertise match, publication history, availability, and conflict-of-interest screening.

### Step 4: Reviewer Assistance
See: `reviewer-perspective.md`

Assist reviewers with structured review generation, statistical checking, citation verification, and consistency analysis — while maintaining strict confidentiality.

### Step 5: Editorial Decision Support

Provide the editor with structured summaries of reviewer reports, highlighting consensus and disagreements, to support (not replace) the editorial decision.

---

## Sub-Files

| File | Purpose |
|---|---|
| `reviewer-perspective.md` | Structured review assistance for peer reviewers |
| `editor-triage.md` | Manuscript screening for editors |
| `integrity-screening.md` | Paper mill detection, image forensics, statistical checks |
| `reviewer-matching.md` | Expertise-based reviewer recommendation |

---

## Skills Used

- `skills/citation-verification.md` — Verify manuscript references
- `skills/statistical-review.md` — Check statistical methods and reporting
- `skills/plagiarism-screening.md` — Text similarity checking
- `skills/image-integrity.md` — Image manipulation detection
- `skills/readability-analysis.md` — Assess manuscript readability

---

## Critical Rules

- `rules/confidentiality.md` — ALL peer review content is confidential
- `rules/quality-gates.md` — STOP-05, STOP-06, STOP-07 are mandatory
- `rules/ai-ethics.md` — AI cannot make editorial decisions
- `rules/citation-integrity.md` — Verify manuscript citations
