# Skill: AI Disclosure Drafting

## Description

Generates publisher-specific AI use disclosure statements based on how AI tools were used during manuscript preparation. Ensures compliance with current publisher policies and places the disclosure in the correct manuscript location.

## When to Use

- During pre-submission (Workflow 02) — STOP-03
- When switching target journals (different publisher, different requirements)
- During revision if AI was used in the revision process
- When updating disclosure after additional AI use

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `publisher` | String | Yes | Target publisher (Elsevier, Springer Nature, Wiley, T&F, SAGE) |
| `journal` | String | Optional | Specific journal (for journal-specific requirements) |
| `ai_tools_used` | List | Yes | Tools with names, versions, and providers |
| `usage_description` | List | Yes | How each tool was used, which sections, for what purpose |
| `human_oversight` | String | Yes | Description of human review and verification |

## Outputs

| Output | Type | Description |
|---|---|---|
| `disclosure_statement` | Text | Publisher-compliant disclosure statement |
| `placement` | String | Where to place in the manuscript (section name) |
| `compliance_checklist` | List | Checklist of compliance requirements (checked/unchecked) |
| `cover_letter_note` | Text | If disclosure is also needed in cover letter |

## Step-by-Step Procedure

### Step 1: Check Publisher Policy

1. Load `config/publisher-policies.yaml`
2. Find the target publisher's current AI policy
3. Check for journal-specific variations (e.g., The Lancet, Cell)
4. Note: `rules/disclosure-compliance.md` for detailed requirements

### Step 2: Catalog AI Usage

Document all AI tool usage:
```yaml
tools:
  - name: "Claude"
    provider: "Anthropic"
    version: "3.5 Sonnet, January 2026"
    purposes:
      - category: "language_editing"
        details: "Grammar and clarity improvement throughout"
        sections: ["Introduction", "Methods", "Discussion"]
      - category: "literature_search"
        details: "Assisted with identifying relevant studies"
        sections: ["Introduction"]
    not_used_for:
      - "Data analysis"
      - "Results interpretation"
      - "Figure generation"
```

### Step 3: Select Template

Load the appropriate template from `templates/`:
- `templates/ai-disclosure-elsevier.md`
- `templates/ai-disclosure-springer.md`
- `templates/ai-disclosure-wiley.md`
- `templates/ai-disclosure-taylor-francis.md`
- `templates/ai-disclosure-sage.md`

### Step 4: Generate Disclosure

Customize the template with specific details:
1. Tool name(s) with version(s)
2. Specific purposes
3. Sections involved
4. Human oversight statement
5. Accountability statement

### Step 5: Determine Placement

| Publisher | Default Placement |
|---|---|
| Elsevier | Dedicated section before References |
| Springer Nature | Methods or Acknowledgements |
| Wiley | Acknowledgements or dedicated section |
| Taylor & Francis | Separate declaration form |
| SAGE | Acknowledgements or Methods |

### Step 6: Author Approval (STOP-03)

Present the disclosure to the author:
- Is it accurate and complete?
- Does it cover ALL AI tools used?
- Is the human oversight description correct?
- Does the author approve the wording?

## Quality Criteria

| Criterion | Standard |
|---|---|
| Publisher compliance | Meets current publisher requirements |
| Specificity | Names specific tools, versions, and purposes |
| Completeness | Covers all AI usage, not just the primary tool |
| Accuracy | Truthfully represents the extent and nature of AI use |
| Placement | Correct location in manuscript per publisher policy |

## Cross-References

- Rules: `rules/disclosure-compliance.md`, `rules/ai-ethics.md`
- Config: `config/publisher-policies.yaml`
- Templates: `templates/ai-disclosure-*.md`
- Workflows: `workflows/02-pre-submission/ai-disclosure-generator.md`
- Agents: Author Agent
