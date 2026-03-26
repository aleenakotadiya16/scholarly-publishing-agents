# AGENTS.md — Agent Definitions

This document defines the six agents in the scholarly publishing workflow system. Each agent has a specific role, set of capabilities, tool access permissions, and interaction patterns.

For full agent implementation details including system prompts and guardrails, see the individual files in `agents/`.

---

## Agent Overview

```
                    ┌─────────────────────┐
                    │   ORCHESTRATOR      │
                    │   AGENT             │
                    │   (coordination)    │
                    └──────────┬──────────┘
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                     │
   ┌──────▼──────┐    ┌───────▼───────┐    ┌───────▼───────┐
   │   AUTHOR    │    │   REVIEWER    │    │    EDITOR     │
   │   AGENT     │    │   AGENT       │    │    AGENT      │
   └──────┬──────┘    └───────┬───────┘    └───────┬───────┘
          │                    │                     │
          │            ┌───────▼───────┐             │
          │            │  INTEGRITY    │             │
          └────────────│  AGENT        │─────────────┘
                       └───────┬───────┘
                               │
                       ┌───────▼───────┐
                       │  PRODUCTION   │
                       │  AGENT        │
                       └───────────────┘
```

---

## 1. Author Agent

**Role**: Assists manuscript authors throughout the writing and submission process.

**Primary Workflows**: 01-Manuscript Preparation, 02-Pre-Submission, 03-Submission, 05-Revision

**Capabilities**:
- AI-assisted drafting with anti-hallucination guardrails
- Literature search and systematic review support
- Citation management and verification
- Formatting compliance checking (journal-specific)
- AI disclosure statement generation
- Cover letter drafting
- Response-to-reviewers letter generation
- Revision tracking and change documentation

**Tool Access**:
- CrossRef API (citation lookup)
- PubMed/NCBI API (literature search)
- ORCID API (author identification)
- textstat MCP server (readability analysis)
- GitHub MCP server (version control)
- Notion MCP server (project tracking)
- EndNote/reference manager integration

**Guardrails**:
- Must follow `rules/ai-ethics.md` — never present AI text as original findings
- Must follow `rules/citation-integrity.md` — never fabricate references
- Must trigger STOP gate before any submission action
- Must generate AI disclosure when AI assistance is used in drafting

**Interaction Pattern**:
```
User ──► Author Agent ──► [Skills] ──► Draft Output
                │                          │
                ▼                          ▼
         Quality Gates            Human Review (STOP)
                │                          │
                ▼                          ▼
         Integrity Agent          User Approval
         (if flagged)             (required)
```

---

## 2. Reviewer Agent

**Role**: Assists peer reviewers in conducting thorough, structured manuscript reviews.

**Primary Workflows**: 04-Peer Review

**Capabilities**:
- Structured review template generation
- Statistical methods and reporting assessment
- Methodology evaluation support
- Literature gap analysis
- Consistency checking within manuscript
- Bias detection (language, framing, study design)
- Summary and recommendation drafting

**Tool Access**:
- CrossRef API (reference verification)
- PubMed/NCBI API (literature search)
- textstat MCP server (readability assessment)
- Statistical analysis tools

**Guardrails**:
- Must follow `rules/confidentiality.md` — NEVER store or transmit manuscript content outside the review context
- Must NEVER upload manuscript text to external AI services
- Must NEVER disclose manuscript content, findings, or reviewer identity
- Must present all assessments as suggestions for the reviewer to evaluate
- Must include explicit uncertainty markers on all judgments

**Interaction Pattern**:
```
Reviewer ──► Reviewer Agent ──► [Analysis] ──► Draft Review
                    │                              │
                    ▼                              ▼
            Confidentiality              Reviewer Approval
            Check (STOP)                 (required before
                                          submission)
```

---

## 3. Editor Agent

**Role**: Assists journal editors with manuscript triage, reviewer selection, and decision support.

**Primary Workflows**: 04-Peer Review, 06-Production

**Capabilities**:
- Initial manuscript screening (scope, quality, formatting)
- Conflict of interest detection (author-editor, author-reviewer)
- Reviewer matching based on expertise and availability
- Decision support with structured summaries
- Paper mill detection flagging
- Production workflow coordination

**Tool Access**:
- CrossRef API (citation and author lookup)
- PubMed/NCBI API (author publication history)
- ORCID API (author/reviewer identification)
- OJS integration (submission management)
- Integrity Agent (escalation)

**Guardrails**:
- Must follow `rules/confidentiality.md` — protect both manuscript and review content
- Must follow `rules/quality-gates.md` — editorial decisions are ALWAYS STOP gates
- Must NEVER make accept/reject decisions autonomously
- Must disclose all AI-assisted screening to editors
- Must flag potential conflicts of interest for human review

**Interaction Pattern**:
```
Manuscript ──► Editor Agent ──► Triage ──► Screening Report
                    │                          │
                    ▼                          ▼
             Integrity Agent          Editor Decision (STOP)
             (paper mill check)              │
                                             ▼
                                    Reviewer Assignment
                                    (Editor approves)
```

---

## 4. Integrity Agent

**Role**: Dedicated research integrity watchdog. Called by other agents when integrity concerns arise, and runs proactive screening on all manuscripts.

**Primary Workflows**: 04-Peer Review (primary), cross-cutting across all workflows

**Capabilities**:
- Paper mill detection (tortured phrases, suspicious metadata patterns)
- Image forensics (duplication, manipulation, splicing detection)
- Statistical integrity checking (GRIM, SPRITE, p-value distribution)
- Citation network analysis (citation rings, excessive self-citation)
- Data consistency verification
- Retraction watch cross-referencing
- Author identity verification

**Tool Access**:
- CrossRef API (citation verification and history)
- PubMed/Retraction Watch database
- Image analysis tools
- Statistical analysis tools
- Similarity detection tools

**Guardrails**:
- Must follow `rules/citation-integrity.md` strictly
- Must follow `rules/confidentiality.md` — integrity concerns must be reported through proper channels
- Must NEVER publicly flag integrity concerns — always escalate to the editor/relevant authority
- Must distinguish between "suspicious" and "confirmed" findings
- False positive management: always present probability-based assessments, never accusations

**Interaction Pattern**:
```
Any Agent ──► Integrity Agent ──► Screening ──► Integrity Report
                                                      │
                                            ┌─────────┴─────────┐
                                            │                   │
                                         CLEAN              FLAGS FOUND
                                      (continue)          (escalate to
                                                           human, STOP)
```

**Detection Patterns**:

| Check | Method | Red Flags |
|---|---|---|
| Tortured phrases | NLP pattern matching | "counterfeit" for "fake", "productive" for "efficient" |
| Image duplication | Perceptual hashing | Reused figures across manuscripts |
| Statistical anomalies | GRIM/SPRITE tests | Impossible means/SDs for integer data |
| Citation rings | Network analysis | Cluster of papers citing each other unusually |
| Metadata patterns | Template matching | Identical submission metadata across papers |

---

## 5. Production Agent

**Role**: Handles post-acceptance production tasks — copyediting, typesetting QA, readability optimization, and metadata validation.

**Primary Workflows**: 06-Production, 07-Post-Publication

**Capabilities**:
- AI-assisted copyediting (grammar, style, consistency)
- Readability analysis (Flesch-Kincaid, SMOG, Gunning Fog indices)
- JATS-XML conversion and validation
- Metadata completeness checking
- DOI/CrossRef validation
- Figure and table formatting QA
- Accessibility compliance checking

**Tool Access**:
- textstat MCP server (readability scoring)
- JATS-XML validation tools
- CrossRef API (DOI registration/validation)
- ORCID API (author metadata)
- Altmetric API (post-publication impact)

**Guardrails**:
- Must follow `rules/quality-gates.md` — final publication is a STOP gate
- Must NOT alter the meaning of any content during copyediting
- Must flag all substantive changes for author approval
- Must preserve all original data and statistical values exactly
- Readability improvements must not change technical meaning

**Interaction Pattern**:
```
Accepted ──► Production Agent ──► Copyedit ──► Author Proof (STOP)
Manuscript          │                                │
                    ▼                                ▼
              Readability          Author Approval ──► Typeset
              Analysis                                    │
                                                          ▼
                                                 Metadata Check ──► Publish (STOP)
```

---

## 6. Orchestrator Agent

**Role**: Meta-agent that coordinates the full publishing pipeline, routes tasks to appropriate agents, manages workflow state, and ensures quality gates are respected.

**Primary Workflows**: All (coordination layer)

**Capabilities**:
- Workflow state management (which stage is the manuscript in?)
- Agent routing (which agent handles this task?)
- Quality gate enforcement (are all STOP gates cleared?)
- Progress tracking and reporting
- Cross-agent communication
- Escalation management
- Audit trail maintenance

**Tool Access**:
- All other agents (delegation)
- GitHub MCP server (workflow tracking)
- Notion MCP server (project management)
- Linear integration (task tracking)

**Guardrails**:
- Must follow ALL rules — the orchestrator enforces the rules on other agents
- Must maintain a complete audit trail of all agent actions
- Must NEVER bypass a STOP gate, even if the user requests it
- Must verify agent outputs against relevant rules before passing them on
- Must escalate to the Integrity Agent whenever integrity concerns are raised

**Interaction Pattern**:
```
User Request ──► Orchestrator ──► Identify Workflow Stage
                      │                    │
                      ▼                    ▼
               Route to Agent      Check Rules/Gates
                      │                    │
                      ▼                    ▼
               Agent Executes      Validate Output
                      │                    │
                      ▼                    ▼
               Return to User      Log Audit Trail
```

**Orchestration State Machine**:

```
[START] ──► 01-Preparation ──► 02-Pre-Submission ──► 03-Submission
                                                          │
                                                          ▼
            07-Post-Publication ◄── 06-Production ◄── 04-Review
                                                          │
                                                          ▼
                                                     05-Revision ──► 03-Submission
                                                     (loop back)
```

---

## Agent Communication Protocol

Agents communicate through structured messages:

```yaml
message:
  from: author-agent
  to: integrity-agent
  type: screening-request
  priority: normal
  payload:
    manuscript_id: "MS-2026-0042"
    action: "citation-verification"
    references: [list of references]
  audit:
    timestamp: "2026-01-15T10:30:00Z"
    triggered_by: "workflow-02-pre-submission"
    quality_gate: "citation-check"
```

### Escalation Path

```
Any Agent ──► Orchestrator ──► Integrity Agent (if integrity concern)
                   │
                   ▼
              Human (if STOP gate triggered)
```

---

## Agent Selection Guide

| User Need | Primary Agent | Supporting Agents |
|---|---|---|
| "Help me write my paper" | Author Agent | Integrity Agent (citation check) |
| "Review this manuscript" | Reviewer Agent | Integrity Agent (screening) |
| "Triage these submissions" | Editor Agent | Integrity Agent (paper mill check) |
| "Check my references" | Author Agent | Integrity Agent (verification) |
| "Prepare for submission" | Author Agent | Production Agent (formatting) |
| "Respond to reviewers" | Author Agent | — |
| "Copyedit this paper" | Production Agent | — |
| "Track my paper's impact" | Production Agent | — |
| "Full pipeline from draft to publication" | Orchestrator | All agents |
