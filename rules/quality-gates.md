# Quality Gates — Human-in-the-Loop Checkpoints

## Overview

Quality gates are checkpoints in the publishing workflow where the system pauses for human review or approval. There are two types:

- **STOP gates** 🛑: Require explicit human approval before the workflow can proceed. The system MUST halt and wait for human input. No agent can bypass a STOP gate.
- **WARN gates** ⚠️: Flag an issue for human attention but do not block workflow progress. The human should review the flag but the workflow can continue if the human acknowledges.

---

## STOP Gates

These gates require explicit human approval. The system must present its work, explain what it found, and wait for the human to approve, modify, or reject before continuing.

### STOP-01: Manuscript Content Approval

**When**: Before any AI-assisted content is incorporated into a manuscript draft
**What**: Human must review all AI-generated or AI-edited text
**Why**: Only humans can take authorship responsibility for content
**Agent**: Author Agent
**Workflow**: 01-Manuscript Preparation

```
AI Draft ──► Present to Author ──► Author Reviews ──► Approve/Edit/Reject
                                                            │
                                                   STOP: Cannot proceed
                                                   until author approves
```

### STOP-02: Citation Verification Sign-off

**When**: After citation verification is complete, before submission
**What**: Human must review the citation verification report and resolve any flagged references
**Why**: Only the author can confirm that references accurately support their claims
**Agent**: Author Agent, Integrity Agent
**Workflow**: 02-Pre-Submission

```
Verification Report ──► Author Reviews ──► Resolves Flags ──► Sign-off
                                                                  │
                                                         STOP: All SUSPICIOUS
                                                         and UNVERIFIED refs
                                                         must be resolved
```

### STOP-03: AI Disclosure Approval

**When**: After AI disclosure statement is generated, before inclusion in manuscript
**What**: Human must review and approve the disclosure statement
**Why**: The disclosure must accurately represent actual AI use; author is accountable
**Agent**: Author Agent
**Workflow**: 02-Pre-Submission

```
Draft Disclosure ──► Author Reviews ──► Accurate? ──► Approve
                                            │
                                    NO ──► Revise ──► Re-review
                                            │
                                   STOP: Inaccurate disclosure
                                   is an ethics violation
```

### STOP-04: Submission Package Approval

**When**: Before any submission action (uploading to journal portal)
**What**: Human must review the complete submission package (manuscript, cover letter, disclosures, metadata, supplementary materials)
**Why**: Submission is an irrevocable action with contractual implications
**Agent**: Author Agent, Orchestrator Agent
**Workflow**: 03-Submission

```
Complete Package ──► Author Reviews ──► All Complete? ──► Submit (human action)
                                             │
                                    NO ──► Fix ──► Re-review
                                             │
                                    STOP: Never auto-submit
```

### STOP-05: Peer Review Submission

**When**: Before a reviewer submits their review to the journal
**What**: Reviewer must review the complete review report, including any AI-assisted analysis
**Why**: The reviewer takes professional responsibility for their review
**Agent**: Reviewer Agent
**Workflow**: 04-Peer Review

```
Draft Review ──► Reviewer Reviews ──► Satisfied? ──► Submit (reviewer action)
                                          │
                                 NO ──► Revise ──► Re-review
                                          │
                                 STOP: Never auto-submit reviews
```

### STOP-06: Editorial Decision

**When**: Before an editor communicates an accept/revise/reject decision
**What**: Editor must make and approve the decision; AI provides decision support only
**Why**: Editorial decisions have career and financial implications; require human judgment
**Agent**: Editor Agent
**Workflow**: 04-Peer Review

```
Decision Support ──► Editor Reviews ──► Makes Decision ──► Communicate
                     (summaries,              │
                      flags,                  │
                      recommendations)  STOP: AI never makes
                                        accept/reject decisions
```

### STOP-07: Integrity Escalation

**When**: When the Integrity Agent flags a potential research integrity concern
**What**: A qualified human (editor, integrity officer) must evaluate the concern
**Why**: False accusations of misconduct can end careers; requires expert judgment
**Agent**: Integrity Agent
**Workflow**: 04-Peer Review (and cross-cutting)

```
Integrity Flag ──► Severity Assessment ──► Escalate to Human
                                                │
                                       STOP: Never publicly flag
                                       integrity concerns without
                                       human expert review
```

### STOP-08: Revision Response Approval

**When**: Before submitting a response-to-reviewers letter
**What**: Author must review point-by-point responses and confirm accuracy
**Why**: Responses represent commitments about what was changed; author is accountable
**Agent**: Author Agent
**Workflow**: 05-Revision

```
Draft Response ──► Author Reviews ──► All Points Addressed? ──► Submit
                                              │
                                     NO ──► Revise ──► Re-review
                                              │
                                     STOP: Incomplete responses
                                     risk rejection
```

### STOP-09: Final Publication Approval

**When**: Before a manuscript is published (author proof stage)
**What**: Author must review final proofs, metadata, and all production changes
**Why**: Post-publication corrections are costly and damaging to reputation
**Agent**: Production Agent
**Workflow**: 06-Production

```
Final Proofs ──► Author Reviews ──► All Correct? ──► Approve for Publication
                                         │
                                NO ──► Request Changes ──► Re-proof
                                         │
                                STOP: Publication is permanent
```

### STOP-10: Erratum/Corrigendum Publication

**When**: Before publishing a correction notice
**What**: All authors must approve the correction notice
**Why**: Corrections are permanent public records; require consensus
**Agent**: Production Agent, Author Agent
**Workflow**: 07-Post-Publication

```
Draft Correction ──► All Authors Review ──► Consensus? ──► Publish Correction
                                                │
                                       NO ──► Negotiate ──► Re-draft
                                                │
                                       STOP: Corrections require
                                       all-author approval
```

---

## WARN Gates

These gates flag issues for human attention but do not block progress. The system continues but displays a clear warning.

### WARN-01: Readability Score Below Threshold

**When**: Readability analysis shows scores below the threshold for the target audience
**What**: Flag specific passages that are too complex for the intended audience
**Agent**: Production Agent, Author Agent
**Threshold**: See `config/quality-thresholds.yaml`

### WARN-02: Statistical Reporting Incomplete

**When**: Statistical review finds missing elements (effect sizes, confidence intervals, etc.)
**What**: Flag missing elements with recommendations
**Agent**: Reviewer Agent, Author Agent
**Threshold**: See `config/quality-thresholds.yaml`

### WARN-03: Formatting Non-compliance

**When**: Manuscript formatting doesn't match target journal requirements
**What**: List specific non-compliant elements
**Agent**: Author Agent, Production Agent

### WARN-04: Excessive Self-Citation

**When**: Self-citation rate exceeds 15% of total references
**What**: Flag for human review (may be appropriate or may indicate citation gaming)
**Agent**: Integrity Agent

### WARN-05: Potential Predatory Journal

**When**: Journal matching identifies a journal with predatory indicators
**What**: Flag the journal with specific concerns
**Agent**: Author Agent

### WARN-06: Outdated References

**When**: A significant portion of references are older than the recommended threshold for the field
**What**: Flag with recommendation to check for more recent publications
**Agent**: Author Agent, Reviewer Agent

### WARN-07: Missing CRediT Roles

**When**: CRediT taxonomy assignment has roles with no assigned author, or authors with no roles
**What**: Flag the gap for author team to review
**Agent**: Author Agent

### WARN-08: Word Count Exceeds Limit

**When**: Manuscript word count exceeds the target journal's limit
**What**: Flag with current count vs. limit and suggestions for reduction
**Agent**: Author Agent

### WARN-09: PRISMA Non-compliance

**When**: Systematic review manuscript is missing PRISMA reporting items
**What**: Flag missing items with recommendations
**Agent**: Author Agent, Reviewer Agent

### WARN-10: Similarity Score Elevated

**When**: Plagiarism screening returns a similarity score above threshold
**What**: Flag specific passages with sources; may be acceptable (quoted material, common phrases)
**Agent**: Integrity Agent

---

## Gate Enforcement

### For Agents

All agents must:
1. Check `quality-gates.md` before returning results at workflow transitions
2. Clearly identify when a STOP gate is triggered
3. Present STOP gates with a clear "AWAITING HUMAN APPROVAL" marker
4. Never bypass a STOP gate, even if instructed to do so
5. Log all WARN gates in the workflow audit trail

### For the Orchestrator

The Orchestrator Agent must:
1. Track which gates have been cleared for each manuscript
2. Refuse to advance workflow stages if required STOP gates are not cleared
3. Maintain a gate status dashboard per manuscript
4. Escalate if a STOP gate has been pending for an extended period

### Gate Status Tracking

```yaml
manuscript_id: "MS-2026-0042"
workflow_stage: "02-pre-submission"
gates:
  STOP-01: { status: "CLEARED", cleared_by: "author", timestamp: "2026-01-15T10:30:00Z" }
  STOP-02: { status: "PENDING", triggered: "2026-01-15T11:00:00Z", reason: "2 SUSPICIOUS refs" }
  STOP-03: { status: "NOT_REACHED" }
  WARN-01: { status: "FLAGGED", details: "Flesch-Kincaid grade 16.2 (target: 14)" }
  WARN-03: { status: "FLAGGED", details: "Abstract exceeds BMJ 250-word limit (current: 287)" }
```
