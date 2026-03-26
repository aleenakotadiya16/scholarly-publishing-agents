# GitHub Copilot Instructions for scholarly-publishing-agents

## Repository Context

This is an agentic workflow system for scholarly publishing — a structured set of rules, workflows, skills, agents, templates, and configurations that guide AI assistants through the full academic publishing lifecycle while maintaining research integrity.

**This is NOT a code library.** Files are Markdown and YAML designed to be read by AI agents and researchers.

## Key Rules for Copilot

### 1. Never Fabricate Citations

When working with references or citations in this repository:
- Do NOT generate citations from your training data — they may be hallucinated
- Do NOT create author names, DOIs, journal names, or publication years
- If asked to add a citation, mark it as `[UNVERIFIED — requires manual lookup]`
- Reference the citation verification skill at `skills/citation-verification.md`

### 2. Respect Publisher Policies

- Check `config/publisher-policies.yaml` before making claims about what publishers require
- Different publishers have different AI disclosure requirements
- Do not assume one publisher's rules apply to another

### 3. Follow Quality Gates

- The `rules/quality-gates.md` file defines STOP and WARN gates
- STOP gates require human approval — never suggest bypassing them
- Include quality gate checks in any workflow modifications

### 4. Maintain Confidentiality

- Per `rules/confidentiality.md`, peer review content is confidential
- Never suggest sending manuscript content to external services
- Never include real manuscript content in code suggestions

### 5. Standards Compliance

When editing or creating content, follow these standards:
- **COPE** guidelines for publication ethics
- **ICMJE** recommendations for medical journal articles
- **CRediT** taxonomy for contributor roles
- **JATS-XML** for article metadata
- **PRISMA** for systematic review reporting

## Repository Structure

```
rules/        — Guardrails (read before any task)
workflows/    — 7 stages: preparation → submission → review → revision → production → publication
agents/       — 6 agent definitions (author, reviewer, editor, integrity, production, orchestrator)
skills/       — 12 reusable skill procedures
templates/    — Publisher-specific templates
config/       — YAML configuration (publisher policies, journal requirements, thresholds)
examples/     — Complete workflow traces
```

## File Conventions

- Content files: `kebab-case.md`
- Config files: `kebab-case.yaml`
- Workflow dirs: `NN-kebab-case/`
- Each workflow directory has a `workflow.md` entry point
- Templates use publisher names or descriptive names

## When Suggesting Changes

1. Ensure all Mermaid diagrams in workflow.md files remain valid
2. Preserve quality gate definitions (STOP/WARN)
3. Cross-reference related files when adding new content
4. Update `skills.md` if adding or modifying skills
5. Update `AGENTS.md` if changing agent capabilities
6. Verify YAML config files remain valid after edits
