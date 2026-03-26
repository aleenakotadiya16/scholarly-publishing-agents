# Workflow 05: Revision

## Overview

This workflow handles the revision process after receiving reviewer feedback — from parsing reviewer comments through point-by-point response generation, revision tracking, and resubmission verification.

**Primary Agent**: Author Agent
**Quality Gates**: STOP-08 (revision response approval)

---

## Workflow Diagram

```mermaid
graph TD
    A[Editor Decision Letter + Reviewer Reports] --> B[Parse Reviewer Comments]
    B --> B1[Categorize Each Comment]
    B1 --> B2[Major Issues]
    B1 --> B3[Minor Issues]
    B1 --> B4[Questions for Clarification]
    B2 --> C[Author Plans Responses]
    B3 --> C
    B4 --> C
    C --> D{Response Type}
    D -->|Agree & Revise| E[Make Revision in Manuscript]
    D -->|Partially Agree| F[Revise + Explain Rationale]
    D -->|Respectfully Disagree| G[Provide Evidence/Rationale]
    D -->|Additional Analysis| H[Conduct New Analysis]
    E --> I[Track Changes in Manuscript]
    F --> I
    G --> I
    H --> I
    I --> J[Draft Point-by-Point Response Letter]
    J --> K[Cross-Check: All Points Addressed?]
    K -->|No| L[Address Missing Points]
    L --> J
    K -->|Yes| M[Verify New References if Added]
    M --> N[Update AI Disclosure if Applicable]
    N --> O{STOP-08: Author Approves Response}
    O -->|Needs Work| P[Revise Response]
    P --> J
    O -->|Approved| Q[Resubmission Verification]
    Q --> R{All Requirements Met?}
    R -->|No| S[Address Gaps]
    S --> Q
    R -->|Yes| T[Resubmission Package → Workflow 03 STOP-04]
```

---

## Steps

### Step 1: Parse and Categorize Reviewer Comments
- Extract individual reviewer comments
- Categorize each as: major issue, minor issue, question, editorial note
- Number each comment for point-by-point tracking

### Step 2: Response Strategy
For each comment, the author decides:
- **Agree and revise**: Make the requested change
- **Partially agree**: Make a modified change with explanation
- **Respectfully disagree**: Provide evidence supporting the original approach
- **Additional work needed**: Conduct new analysis, add data, etc.

### Step 3: Point-by-Point Response
See: `response-to-reviewers.md`
- Draft a structured response addressing every single comment
- Include specific manuscript locations for all changes
- Use professional, respectful tone throughout

### Step 4: Revision Tracking
See: `revision-tracking.md`
- Track all changes in the manuscript
- Maintain a change log with locations and reasons
- Prepare both clean and tracked-changes versions

### Step 5: Resubmission Verification
See: `resubmission-check.md`
- Verify every reviewer point has a response
- Verify all promised changes are in the manuscript
- Check for new references added during revision
- Update AI disclosure if AI was used during revision

---

## Sub-Files

| File | Purpose |
|---|---|
| `response-to-reviewers.md` | Point-by-point response drafting |
| `revision-tracking.md` | Change tracking and documentation |
| `resubmission-check.md` | Final verification before resubmission |

---

## Skills Used

- `skills/response-letter-drafting.md` — Structured response generation
- `skills/citation-verification.md` — Verify any new references
- `skills/statistical-review.md` — If additional analyses conducted
- `skills/ai-disclosure-drafting.md` — Update disclosure if AI used in revision
