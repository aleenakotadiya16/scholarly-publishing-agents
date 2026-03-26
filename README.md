# scholarly-publishing-agents

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![COPE](https://img.shields.io/badge/COPE-Compliant-green.svg)](https://publicationethics.org/)
[![JATS](https://img.shields.io/badge/JATS--XML-1.3-orange.svg)](https://jats.nlm.nih.gov/)
[![CRediT](https://img.shields.io/badge/CRediT-Taxonomy-purple.svg)](https://credit.niso.org/)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Compatible-blueviolet.svg)]()
[![Cursor](https://img.shields.io/badge/Cursor-Compatible-blue.svg)]()
[![Copilot](https://img.shields.io/badge/GitHub_Copilot-Compatible-black.svg)]()

**An agentic workflow system for the full scholarly publishing lifecycle — from manuscript preparation through post-publication impact tracking.**

Built for researchers, reviewers, editors, and publishers who want AI assistance without compromising research integrity.

---

## Problem Statement

Academic publishing faces three interlocking categories of problems that this system addresses:

### 1. AI Pitfalls in Scholarly Work

- **Hallucinated citations**: GPTZero found 100+ hallucinated citations across 53 papers at NeurIPS 2025. A Deakin University study found ChatGPT fabricated ~20% of academic citations.
- **Fabricated references**: AI models blend real papers, invent authors, paraphrase titles, and create fake journals.
- **Training data contamination**: "AI-on-AI" feedback loops risk polluting future training data (model collapse).
- **Lack of epistemic awareness**: Models cannot recognize when they are hallucinating.
- **Subtle fabrication**: Fake citations that look plausible defeat naive fact-checking.

### 2. Systemic Publishing Problems

- **Paper mills**: Mass-produced fabricated studies doubling output every 1.5 years. Wiley/Hindawi retracted 11,300+ papers at an $18M revenue hit.
- **Peer review overload**: NeurIPS received 21,575 submissions in 2025 (up from 12,343 in 2023). Deep scrutiny is becoming impossible.
- **Slow publication timelines**: Average review cycles of 12+ weeks.
- **Inconsistent compliance**: Authors struggle with publisher-specific formatting, disclosure, and metadata requirements.
- **Research integrity gaps**: Fabricated data, duplicated images, manipulated peer review, sold authorship slots.

### 3. Stakeholder Pain Points

| Stakeholder | Pain Points |
|---|---|
| **Authors** | Citation management, formatting compliance, disclosure requirements, revision tracking |
| **Reviewers** | Review fatigue, structural consistency, statistical verification, integrity checks |
| **Editors** | Triage volume, reviewer matching, conflict detection, paper mill screening |
| **Publishers** | Policy enforcement, metadata quality, production delays, integrity at scale |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                     ORCHESTRATOR AGENT                              │
│                   (coordination + routing)                          │
│    ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌──────────┐ ┌──────────┐ │
│    │ Author  │ │Reviewer │ │ Editor  │ │Integrity │ │Production│ │
│    │ Agent   │ │ Agent   │ │ Agent   │ │  Agent   │ │  Agent   │ │
│    └────┬────┘ └────┬────┘ └────┬────┘ └────┬─────┘ └────┬─────┘ │
│         │           │           │            │            │        │
└─────────┼───────────┼───────────┼────────────┼────────────┼────────┘
          │           │           │            │            │
┌─────────▼───────────▼───────────▼────────────▼────────────▼────────┐
│                         SKILLS LAYER                                │
│  ┌──────────────┐ ┌─────────────┐ ┌────────────┐ ┌──────────────┐ │
│  │  Citation     │ │ Readability │ │ Statistical│ │  Plagiarism  │ │
│  │  Verification │ │ Analysis    │ │ Review     │ │  Screening   │ │
│  ├──────────────┤ ├─────────────┤ ├────────────┤ ├──────────────┤ │
│  │  Image        │ │ JATS-XML    │ │ Journal    │ │ AI Disclosure│ │
│  │  Integrity    │ │ Conversion  │ │ Matching   │ │ Drafting     │ │
│  ├──────────────┤ ├─────────────┤ ├────────────┤ ├──────────────┤ │
│  │  CRediT       │ │ PRISMA      │ │ Cover      │ │ Response     │ │
│  │  Taxonomy     │ │ Compliance  │ │ Letter     │ │ Letter       │ │
│  └──────────────┘ └─────────────┘ └────────────┘ └──────────────┘ │
└────────────────────────────────────────────────────────────────────┘
          │                                                │
┌─────────▼────────────────────────────────────────────────▼─────────┐
│                        RULES & GUARDRAILS                          │
│  AI Ethics │ Citation Integrity │ Disclosure │ Confidentiality     │
│            │                    │ Compliance │ Quality Gates       │
└────────────────────────────────────────────────────────────────────┘
          │                                                │
┌─────────▼────────────────────────────────────────────────▼─────────┐
│                     WORKFLOWS (7 stages)                           │
│  01 Manuscript │ 02 Pre-Sub │ 03 Submit │ 04 Review │ 05 Revise  │
│  Preparation   │            │           │           │             │
│                            06 Production │ 07 Post-Publication    │
└────────────────────────────────────────────────────────────────────┘
          │                                                │
┌─────────▼────────────────────────────────────────────────▼─────────┐
│                    EXTERNAL INTEGRATIONS                            │
│  CrossRef │ PubMed │ DOI │ ORCID │ Altmetric │ OSF │ EndNote     │
│  GitHub MCP │ Notion MCP │ textstat MCP │ Linear │ OJS          │
└────────────────────────────────────────────────────────────────────┘
```

### Design Principles

1. **Human-in-the-loop at every critical juncture** — No autonomous decisions on content, claims, or data
2. **Citation verification as first-class concern** — Every reference must be verifiable against CrossRef/PubMed/DOI
3. **Publisher-agnostic with publisher-specific modules** — Core logic works universally; templates adapt per publisher
4. **Transparency by default** — All AI involvement is documented and disclosed
5. **Multi-stakeholder** — Serves authors, reviewers, editors, and publishers
6. **Composable** — Skills and workflows can be used independently or orchestrated together
7. **Standards-compliant** — JATS-XML, CRediT, COPE, ICMJE, PRISMA
8. **Defensive against AI pitfalls** — Built-in guards against hallucination, fabrication, and bias

---

## Getting Started

### Prerequisites

- An agentic coding tool: [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [Cursor](https://cursor.sh/), [GitHub Copilot](https://github.com/features/copilot), [Gemini CLI](https://github.com/google-gemini/gemini-cli), or [Codex](https://openai.com/codex)
- Optional MCP servers for enhanced functionality:
  - `textstat` MCP server (readability analysis)
  - GitHub MCP server (repo management)
  - Notion MCP server (project tracking)

### Installation

```bash
# Clone the repository
git clone https://github.com/edithatogo/scholarly-publishing-agents.git
cd scholarly-publishing-agents
```

### Usage with Claude Code

```bash
# Claude Code automatically reads CLAUDE.md for context
claude

# Then ask:
# "Help me prepare my manuscript on health economics for submission to BMJ"
# "Run a citation verification on my reference list"
# "Generate an AI disclosure statement for Elsevier"
```

### Usage with Cursor

Cursor automatically loads `.cursor/rules/scholarly-publishing.mdc` for context. Open the repo and start working — the rules are injected into every conversation.

### Usage with GitHub Copilot

Copilot reads `.github/copilot-instructions.md` for repo-specific context. Use Copilot Chat with `@workspace` to leverage the full system.

### Usage with Gemini CLI / Codex

Point the tool at `AGENTS.md` or specific workflow files for context:

```bash
# Gemini CLI
gemini --context AGENTS.md "Review my manuscript for statistical reporting completeness"

# Codex
codex --file AGENTS.md "Check my references against CrossRef"
```

---

## Repository Structure

| Directory | Purpose |
|---|---|
| `rules/` | Shared guardrails — AI ethics, citation integrity, disclosure compliance, confidentiality, quality gates |
| `workflows/` | 7 end-to-end workflows covering the full publishing lifecycle |
| `agents/` | 6 agent definitions with system prompts, tool access, and interaction patterns |
| `skills/` | 12 reusable skill definitions with procedures, quality criteria, and cross-references |
| `templates/` | 9 ready-to-use templates for disclosures, reviews, cover letters, checklists |
| `config/` | YAML configuration for publisher policies, journal requirements, quality thresholds |
| `examples/` | 3 complete workflow traces demonstrating real usage scenarios |

---

## Workflows at a Glance

| # | Workflow | Key Capabilities |
|---|---|---|
| 01 | Manuscript Preparation | AI-assisted drafting with anti-hallucination guards, literature review, formatting |
| 02 | Pre-Submission | Self-review checklist, reference validation, AI disclosure generation, metadata prep |
| 03 | Submission | Journal selection, cover letter generation, submission package assembly |
| 04 | Peer Review | Reviewer assistance, editor triage, integrity screening, reviewer matching |
| 05 | Revision | Point-by-point response, revision tracking, resubmission verification |
| 06 | Production | Copyediting with readability analysis, typesetting QA, metadata validation |
| 07 | Post-Publication | Impact tracking, erratum/corrigendum workflow, plain-language dissemination |

---

## Standards & Compliance

This system is built around established scholarly publishing standards:

- **[COPE](https://publicationethics.org/)** — Committee on Publication Ethics guidelines
- **[ICMJE](https://www.icmje.org/)** — International Committee of Medical Journal Editors recommendations
- **[CRediT](https://credit.niso.org/)** — Contributor Roles Taxonomy (NISO Z39.104)
- **[JATS-XML](https://jats.nlm.nih.gov/)** — Journal Article Tag Suite
- **[PRISMA](http://www.prisma-statement.org/)** — Preferred Reporting Items for Systematic Reviews
- **[ORCID](https://orcid.org/)** — Open Researcher and Contributor ID

---

## MCP Server Integration

The system integrates with Model Context Protocol (MCP) servers for enhanced tool access:

| MCP Server | Function | Used By |
|---|---|---|
| `textstat` | Readability scoring (Flesch-Kincaid, SMOG, Gunning Fog) | Production Agent, Readability Analysis skill |
| `github` | Repository management, issue tracking | Orchestrator Agent |
| `notion` | Project tracking, knowledge base | Orchestrator Agent |
| CrossRef API | Citation verification, DOI resolution | Citation Verification skill |
| PubMed API | Literature search, reference validation | Literature Review workflow |
| ORCID API | Author identification | Metadata Preparation workflow |

---

## Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork the repository** and create a feature branch
2. **Follow existing conventions** — see `CLAUDE.md` for repo structure and style
3. **Test your workflows** with at least one agentic coding tool
4. **Respect scholarly publishing ethics** — all contributions must align with COPE guidelines
5. **Document thoroughly** — every skill, workflow, and rule should be self-documenting
6. **Submit a pull request** with a clear description of changes

### Priority Areas for Contribution

- Additional publisher-specific templates and policies
- Journal requirement configurations for more journals
- Translations of templates for non-English publishing
- Integration patterns for additional MCP servers
- Workflow extensions for specific disciplines (clinical trials, systematic reviews)

---

## License

MIT License — see [LICENSE](LICENSE) for details.

Copyright (c) 2026 Dylan A. Mordaunt
