# Skill: Response Letter Drafting

## Description

Assists in drafting point-by-point response letters to reviewer and editor comments. Ensures every comment is addressed with specific, professional responses and clear manuscript location references.

## When to Use

- After receiving a revise decision (Workflow 05)
- When resubmitting a revised manuscript
- When responding to post-publication comments

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `editor_comments` | Text | Yes | Editor's decision letter comments |
| `reviewer_comments` | List | Yes | All reviewer reports |
| `revision_notes` | Object | Yes | Author's notes on how each point was addressed |
| `revised_manuscript` | Text | Optional | For cross-referencing page/line numbers |

## Outputs

| Output | Type | Description |
|---|---|---|
| `response_letter` | Text | Complete point-by-point response |
| `completeness_check` | Object | Every comment mapped to a response |
| `change_summary` | Text | Summary of all changes made |

## Step-by-Step Procedure

### Step 1: Parse All Comments

Extract and number each individual comment:
```yaml
comments:
  editor:
    - id: "E-1"
      text: "Please address Reviewer 2's concerns about sample size"
      type: "directive"
  reviewer_1:
    - id: "R1-1"
      text: "The statistical approach is not justified"
      type: "major"
    - id: "R1-2"
      text: "Table 2 is unclear"
      type: "minor"
  reviewer_2:
    - id: "R2-1"
      text: "Sample size appears insufficient"
      type: "major"
```

### Step 2: Map Author Responses

For each comment, identify the author's response strategy:
- **Agree and revise**: What change was made, where
- **Partially agree**: What was changed, what wasn't, why
- **Respectfully disagree**: Evidence supporting original approach
- **Additional work**: What new analysis or content was added

### Step 3: Draft Responses

For each comment, draft a professional response:

1. Thank the reviewer for the specific point
2. Directly address the concern
3. Describe what was changed (if anything)
4. Reference specific page/line numbers in the revised manuscript
5. Provide evidence if disagreeing

### Step 4: Format the Letter

Use the structure from `templates/response-to-reviewers-template.md`:
- Opening paragraph thanking the editor and reviewers
- Organized by reviewer (Editor → Reviewer 1 → Reviewer 2 → ...)
- Each comment in bold, followed by the response
- Change locations clearly referenced

### Step 5: Completeness Verification

Create a cross-reference matrix:

| Comment | Response | Change Location | Verified |
|---|---|---|---|
| E-1 | Addressed via R2-1 response | N/A | ✅ |
| R1-1 | Added justification | Page 8, L167-175 | ✅ |
| R1-2 | Reformatted table | Table 2 | ✅ |
| R2-1 | Added power analysis | Page 9, L190-198 | ✅ |

**Every row must show ✅ before the letter is complete.**

### Step 6: Quality Check

- [ ] Every single comment has a response (no omissions)
- [ ] Responses are specific (not vague)
- [ ] Page/line numbers are correct for the revised manuscript
- [ ] Tone is professional and respectful throughout
- [ ] Evidence provided when disagreeing
- [ ] New references (if any) are verified
- [ ] Summary of major changes included at the end

## Quality Criteria

| Criterion | Standard |
|---|---|
| Completeness | 100% of comments addressed |
| Specificity | Every response references specific manuscript locations |
| Tone | Professional, grateful, non-defensive |
| Accuracy | Promised changes are actually in the manuscript |
| Verification | Cross-reference matrix complete |

## Cross-References

- Templates: `templates/response-to-reviewers-template.md`
- Workflows: `workflows/05-revision/response-to-reviewers.md`
- Agents: Author Agent
- Rules: `rules/quality-gates.md` (STOP-08)
