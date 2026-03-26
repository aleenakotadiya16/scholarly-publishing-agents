# Skill: Cover Letter Drafting

## Description

Generates evidence-based cover letters tailored to specific journals. Highlights manuscript significance, relevance to journal scope, and key findings while avoiding generic language.

## When to Use

- During submission preparation (Workflow 03)
- When switching target journals after rejection
- When an editor requests a revised cover letter

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `manuscript_abstract` | Text | Yes | Manuscript abstract |
| `target_journal` | String | Yes | Name of the target journal |
| `key_findings` | List | Yes | 3-5 key findings of the manuscript |
| `author_info` | Object | Yes | Corresponding author name, title, institution |
| `special_considerations` | List | Optional | Invited submission, special issue, etc. |
| `suggested_reviewers` | List | Optional | 3-5 suggested reviewers with rationale |
| `excluded_reviewers` | List | Optional | Reviewers to exclude with brief reason |

## Outputs

| Output | Type | Description |
|---|---|---|
| `cover_letter` | Text | Complete cover letter draft |
| `customization_notes` | List | Journal-specific elements included |
| `checklist` | List | Required cover letter elements (checked/unchecked) |

## Step-by-Step Procedure

### Step 1: Research the Journal

1. Check `config/journal-requirements.yaml` for cover letter requirements
2. Identify the editor-in-chief or handling editor (from journal website)
3. Find 2-3 recent related articles published in the journal (for relevance argument)
4. Note any special requirements (AI disclosure in cover letter, structured format)

### Step 2: Draft Opening

- Address the editor by name if known
- State the manuscript title and article type
- Include the standard exclusivity declaration

### Step 3: Articulate Significance

- What knowledge gap does this work fill?
- Why does it matter? (clinical impact, policy relevance, methodological advance)
- What are the main findings? (concise, specific)
- How does it advance the field?

### Step 4: Connect to Journal

- Why this journal specifically? (scope, audience, recent publications)
- Reference 1-2 related papers published in the journal (VERIFIED citations only)
- Explain how this manuscript serves the journal's readership

### Step 5: Include Required Declarations

Per journal requirements:
- Ethical approvals
- Author consent and contributions
- COI disclosure
- AI disclosure (if required — e.g., The Lancet)
- Data availability
- Funding

### Step 6: Add Reviewer Suggestions (if applicable)

For each suggested reviewer:
- Full name, institution, email
- Brief rationale (1 sentence on why they're qualified)
- Confirmation of no conflicts

### Step 7: Finalize and Quality Check

- [ ] Editor name correct and current
- [ ] Journal name correct (no mixups from previous submissions!)
- [ ] Manuscript title matches the actual manuscript
- [ ] All required elements present per journal guidelines
- [ ] No AI-generated citations that haven't been verified
- [ ] Professional tone, not obsequious
- [ ] Length appropriate (typically < 1 page body)

## Quality Criteria

| Criterion | Standard |
|---|---|
| Specificity | Clearly tailored to the target journal (not generic) |
| Accuracy | Key findings accurately represent manuscript results |
| Completeness | All journal-required elements present |
| Tone | Professional, confident without overselling |
| Length | Concise — typically under 500 words body text |

## Cross-References

- Templates: `templates/cover-letter-template.md`
- Workflows: `workflows/03-submission/cover-letter.md`
- Config: `config/journal-requirements.yaml`
- Agents: Author Agent
