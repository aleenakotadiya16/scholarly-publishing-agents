# CLAUDE.md — Agent Instructions for scholarly-publishing-agents

> This file provides context and instructions for Claude Code (and other AI coding agents) working in this repository.

## Repository Purpose

This is an **agentic workflow system for scholarly publishing** — a structured set of rules, workflows, skills, agents, templates, and configurations that guide AI assistants through the full academic publishing lifecycle while maintaining research integrity.

**This is NOT a code library.** It is a knowledge-and-workflow repository. Files are primarily Markdown and YAML, designed to be read by AI agents and human researchers.

---

## Repository Structure

```
scholarly-publishing-agents/
├── CLAUDE.md              ← You are here
├── AGENTS.md              # Agent definitions (6 agents)
├── skills.md              # Master skill index (12 skills)
├── rules/                 # Guardrails — ALWAYS consult before generating content
│   ├── ai-ethics.md       # COPE + publisher ethics rules
│   ├── citation-integrity.md   # Anti-hallucination citation rules
│   ├── disclosure-compliance.md # Publisher-specific disclosure requirements
│   ├── confidentiality.md      # Peer review confidentiality
│   └── quality-gates.md        # STOP/WARN human-in-the-loop gates
├── workflows/             # 7 sequential workflow stages
│   ├── 01-manuscript-preparation/
│   ├── 02-pre-submission/
│   ├── 03-submission/
│   ├── 04-peer-review/
│   ├── 05-revision/
│   ├── 06-production/
│   └── 07-post-publication/
├── agents/                # 6 agent definitions with system prompts
├── skills/                # 12 reusable skill definitions
├── templates/             # 9 document templates
├── config/                # YAML configuration files
└── examples/              # 3 complete workflow traces
```

---

## Key Conventions

### 1. Rules Are Mandatory

Before performing ANY scholarly publishing task, consult the relevant rules in `rules/`. These are not suggestions — they are guardrails:

- **Before generating any citation**: Read `rules/citation-integrity.md`
- **Before drafting any content**: Read `rules/ai-ethics.md`
- **Before handling any manuscript under review**: Read `rules/confidentiality.md`
- **Before any publisher interaction**: Read `rules/disclosure-compliance.md`
- **At every decision point**: Check `rules/quality-gates.md` for STOP/WARN gates

### 2. Workflow Navigation

Workflows are numbered sequentially (01-07) and each has a `workflow.md` entry point. When helping a user:

1. Identify which workflow stage they're in
2. Read the relevant `workflow.md` first
3. Follow the sub-files for specific tasks
4. Check quality gates before advancing to the next stage

### 3. Skills Are Composable

Skills in `skills/` are standalone procedures. They can be:
- Called directly by a user ("verify my citations")
- Invoked by a workflow step
- Combined by the orchestrator agent

Always read the full skill definition before executing it.

### 4. Templates Are Starting Points

Templates in `templates/` provide structure. They should be:
- Filled in with real, verified information
- Adapted to the specific journal/publisher
- Never submitted with placeholder text still present

### 5. Configuration Is Authoritative

YAML files in `config/` contain structured data about publisher policies, journal requirements, and quality thresholds. **Always check these before making claims about what a publisher requires.**

---

## Anti-Hallucination Guardrails

### CRITICAL: Citation Rules

1. **NEVER fabricate a citation.** If you cannot verify a reference exists, say so explicitly.
2. **NEVER guess author names, journal names, DOIs, or publication years.** Look them up or ask the user.
3. **NEVER blend two real papers into one fake reference.**
4. **ALWAYS flag uncertainty** — if you're not sure a reference is real, mark it with `[UNVERIFIED]`.
5. **Prefer "I don't have this reference" over fabricating one.**

### Content Generation Rules

1. **NEVER present AI-generated text as original research findings.**
2. **NEVER fabricate data, statistics, or experimental results.**
3. **ALWAYS distinguish between** what the user's manuscript says vs. what you're suggesting.
4. **ALWAYS recommend human verification** of factual claims.
5. **Mark all AI-generated content** so the user can review and attribute appropriately.

### Publisher Policy Rules

1. **NEVER claim a publisher allows something without checking `config/publisher-policies.yaml`.**
2. **Policies change** — always recommend the user verify current requirements on the publisher's website.
3. **When in doubt, disclose more** rather than less.

---

## How to Use This Repo as an Agent

### Scenario: User wants help preparing a manuscript

```
1. Read rules/ai-ethics.md (understand what you can/cannot do)
2. Read workflows/01-manuscript-preparation/workflow.md
3. Follow the workflow steps, invoking skills as needed
4. Check rules/quality-gates.md at each decision point
5. When the user is ready to submit, transition to workflow 02
```

### Scenario: User wants to verify their references

```
1. Read rules/citation-integrity.md
2. Read skills/citation-verification.md
3. Execute the verification procedure
4. Report results with confidence levels
5. Flag any unverifiable references
```

### Scenario: User needs an AI disclosure statement

```
1. Read rules/disclosure-compliance.md
2. Check config/publisher-policies.yaml for the target publisher
3. Read skills/ai-disclosure-drafting.md
4. Use the appropriate template from templates/
5. Customize for the user's specific AI usage
```

---

## MCP Server Integration

If MCP servers are available in the user's environment, use them:

| MCP Server | Use For |
|---|---|
| `textstat` | Readability scoring (Flesch-Kincaid, SMOG, Gunning Fog) |
| `github` | Repository management, issue tracking, PR workflows |
| `notion` | Project tracking, knowledge management |
| CrossRef API | Citation verification via DOI lookup |
| PubMed/NCBI API | Literature search and reference validation |

### Checking MCP Availability

If using Claude Code, check for available MCP servers at the start of a session. Adapt your approach based on what's available — the workflows are designed to work with or without MCP servers.

---

## Agent Roles (Summary)

See `AGENTS.md` for full definitions. Quick reference:

| Agent | Primary Role |
|---|---|
| **Author Agent** | Assists manuscript authors with drafting, formatting, citation management |
| **Reviewer Agent** | Assists peer reviewers with structured review, statistical checking |
| **Editor Agent** | Assists editors with triage, reviewer matching, decision support |
| **Integrity Agent** | Dedicated to research integrity — paper mills, image forensics, data checks |
| **Production Agent** | Copyediting, typesetting QA, readability analysis, metadata validation |
| **Orchestrator Agent** | Coordinates the pipeline, routes tasks to appropriate agents |

---

## Common Mistakes to Avoid

1. **Do not skip quality gates.** The `STOP` gates in `rules/quality-gates.md` require human approval.
2. **Do not assume publisher policies.** Always check `config/publisher-policies.yaml`.
3. **Do not generate citations from memory.** Always verify against external databases.
4. **Do not process peer review manuscripts through AI without explicit permission.** See `rules/confidentiality.md`.
5. **Do not present AI suggestions as the user's own analysis.** Maintain clear attribution.
6. **Do not auto-submit anything.** All submissions require explicit human action.

---

## File Naming Conventions

- Workflow directories: `NN-kebab-case/` (e.g., `01-manuscript-preparation/`)
- All content files: `kebab-case.md`
- Config files: `kebab-case.yaml`
- Templates: `descriptive-name-template.md` or `ai-disclosure-publisher.md`

---

## Cross-Tool Compatibility

This repository is designed to work with multiple AI coding tools:

| Tool | Entry Point | Auto-loaded |
|---|---|---|
| Claude Code | `CLAUDE.md` | Yes (automatic) |
| Cursor | `.cursor/rules/scholarly-publishing.mdc` | Yes (automatic) |
| GitHub Copilot | `.github/copilot-instructions.md` | Yes (via @workspace) |
| Gemini CLI | `AGENTS.md` (pass as context) | Manual |
| Codex | `AGENTS.md` (pass as context) | Manual |
