# Reviewer Perspective — Structured Review Assistance

## Purpose

Assist peer reviewers in conducting thorough, structured manuscript reviews while maintaining strict confidentiality. The AI provides analytical support; the reviewer provides expert judgment.

---

## Critical Confidentiality Notice

**Before using AI assistance for peer review, verify**:
1. The journal permits AI-assisted reviewing (most do NOT permit uploading to external AI)
2. You are using AI within a local/private environment that does not transmit manuscript content externally
3. See `rules/confidentiality.md` for full confidentiality requirements

---

## Structured Review Framework

### 1. Summary Assessment

Guide the reviewer to produce:
- A 2-3 sentence summary of the manuscript's main claims and findings
- Assessment of the manuscript's significance to the field
- Overall recommendation (accept / minor revisions / major revisions / reject)

### 2. Major Issues

Help identify and articulate:
- **Methodological concerns**: Study design, sample size, bias, confounding
- **Analytical issues**: Inappropriate statistical methods, missing analyses
- **Interpretation problems**: Conclusions not supported by data, overclaiming
- **Integrity concerns**: Suspicious data patterns, citation issues, potential plagiarism
- **Structural problems**: Missing sections, illogical flow, inadequate literature review

### 3. Minor Issues

Help identify:
- Grammar and language issues
- Formatting inconsistencies
- Minor citation errors
- Table/figure labeling issues
- Missing minor details

### 4. Statistical Review Support

Using `skills/statistical-review.md`:
- Are statistical tests appropriate for the data type?
- Are assumptions tested and reported?
- Are effect sizes and confidence intervals reported?
- Are multiple comparisons addressed?
- Are sample sizes adequate (power analysis)?
- Do the numbers add up (GRIM test for integer data)?

### 5. Citation Spot-Check

The reviewer can ask the agent to verify a subset of key citations:
- Do the cited papers actually say what the authors claim?
- Are key citations real and accurately referenced?
- Are there obvious missing citations (landmark papers in the field)?
- Are self-citations excessive? (WARN-04 if >15%)

### 6. Consistency Check

- Do numbers in the text match the tables?
- Do percentages add up correctly?
- Are all figures referenced in the text?
- Are all tables referenced in the text?
- Does the abstract accurately reflect the full paper?
- Are the conclusions supported by the results section?

---

## Review Output Template

See `templates/reviewer-report-template.md` for the structured output template.

### Structured Review Format

```markdown
## Reviewer Report

### Summary
[2-3 sentence summary of the paper]

### Overall Assessment
**Recommendation**: [Accept / Minor Revisions / Major Revisions / Reject]
**Confidence**: [High / Medium / Low]

### Significance
[Assessment of the contribution to the field]

### Major Issues
1. [Issue description, location in manuscript, suggested resolution]
2. [Issue description, location in manuscript, suggested resolution]

### Minor Issues
1. [Issue, location, suggestion]
2. [Issue, location, suggestion]

### Questions for Authors
1. [Specific question requiring clarification]

### Statistical Assessment
[Summary of statistical review findings]

### Ethics and Integrity
[Any concerns about ethics, integrity, or compliance]

### Recommendation Summary
[Final summary supporting the recommendation]
```

---

## Reviewer Assistance Boundaries

### AI CAN:
- Help structure the review document
- Check statistical methods against best practices
- Verify citations against external databases
- Check internal consistency of numbers
- Identify potentially missing references in the field
- Flag common methodological issues
- Help articulate concerns clearly and professionally
- Generate checklists based on reporting guidelines (CONSORT, STROBE, PRISMA)

### AI MUST NOT:
- Make the final recommendation (reviewer's expert judgment)
- Upload manuscript content to external services
- Store manuscript content beyond the review session
- Bias the review with pre-existing knowledge about the authors
- Generate fabricated concerns or praise
- Replace the reviewer's domain expertise
- Communicate with the authors or editor directly
