# Example: Reviewer Workflow

## Scenario

A peer reviewer has been invited to review a manuscript on digital health interventions for a medical journal. They want AI assistance to conduct a thorough, structured review while maintaining strict confidentiality.

---

## Workflow Trace

### Pre-Review Setup

**User**: "I've been asked to review a paper on digital health interventions for BMJ Digital Health. Can you help me structure my review?"

**Orchestrator Agent** → Routes to **Reviewer Agent**

**Reviewer Agent Actions**:

1. **Confidentiality Check** (`rules/confidentiality.md`):
   ```
   ⚠️ CONFIDENTIALITY NOTICE
   Before proceeding, please confirm:
   1. Does BMJ Digital Health permit AI-assisted reviewing?
   2. We will process the manuscript locally only — no content will be
      sent to external services.
   3. I will not store any manuscript content beyond this session.

   Note: Most journals do NOT currently permit reviewers to upload
   manuscripts to AI tools. Please verify with the journal.
   ```
   **Reviewer**: Confirms they will process locally within their private environment.

2. **Load Review Framework**:
   - Identifies article type: Original Research (RCT)
   - Loads CONSORT checklist for RCT assessment
   - Prepares structured review template: `templates/reviewer-report-template.md`

### Review Analysis

**Reviewer Agent** analyzes the manuscript (all processing local):

3. **Structural Assessment**:
   ```
   STRUCTURAL ANALYSIS
   ✅ All IMRAD sections present
   ✅ Abstract matches main text claims
   ✅ Methods sufficiently detailed
   ⚠️ Results: Not all secondary outcomes reported in text (Table 3 has outcomes not discussed)
   ⚠️ Discussion: Limitations section brief (2 sentences)
   ```

4. **CONSORT Compliance Check** (reporting guideline):
   ```
   CONSORT 2010 COMPLIANCE: 19/25 items reported

   Missing items:
   - Item 3b: Important changes to methods after trial commencement (not reported)
   - Item 6a: How sample size was determined (power analysis not described)
   - Item 13a: Flow of participants through each stage (CONSORT diagram mentioned but not included)
   - Item 14b: Why the trial ended (not stated)
   - Item 17b: Unintended effects or harms (not addressed)
   - Item 25: Where the trial protocol can be accessed (not provided)
   ```

5. **Statistical Assessment** (`skills/statistical-review.md`):
   ```
   STATISTICAL REVIEW

   Methods Used: ITT analysis, mixed-effects models, chi-square tests
   Software: Stata 17.0 (identified ✅)

   Findings:
   ✅ Primary analysis appropriate (mixed-effects for repeated measures)
   ✅ P-values reported as exact values
   ⚠️ Effect sizes not reported for secondary outcomes
   ⚠️ No sample size justification / power analysis
   ⚠️ Multiple secondary outcomes tested (n=5) without multiplicity adjustment
   ✅ GRIM test: All means consistent with sample sizes
   ✅ Internal consistency: Percentages sum correctly

   Concern: Table 2, Column 4 — the 95% CI [-0.15, 0.38] does not contain
   the reported point estimate (0.42). This appears to be an error.
   ```

6. **Citation Spot-Check** (5 key references via DOI lookup):
   ```
   CITATION SPOT-CHECK (5 key references)

   Ref #3 (Smith et al., 2023): VERIFIED ✅
   Ref #8 (WHO, 2022): VERIFIED ✅
   Ref #15 (Chen et al., 2024): VERIFIED ✅ (but year in text says 2023, ref list says 2024)
   Ref #22 (Digital Health Foundation, 2023): NOT FOUND ❌
     - No record in CrossRef, PubMed, or OpenAlex
     - Organization "Digital Health Foundation" not identifiable
     - SUSPICIOUS: May be a hallucinated or fabricated reference
   Ref #31 (Australian Government, 2024): VERIFIED ✅
   ```

7. **Consistency Analysis**:
   ```
   CONSISTENCY CHECK
   ✅ Abstract claims match results section
   ✅ Table 1 totals match reported N (n=245)
   ⚠️ Table 2, Col 4: CI does not contain point estimate (error)
   ⚠️ Text says "12-month follow-up" but Table 3 header says "6-month follow-up"
   ✅ All figures referenced in text are present
   ⚠️ Supplementary Table S2 referenced in text but not provided
   ```

### Review Drafting

8. **Generate Draft Review**:

The Reviewer Agent presents its analysis to the reviewer:

```markdown
## Analysis for Reviewer Consideration

Based on my analysis, here are potential issues for your consideration.
Please evaluate each finding and decide whether and how to include
it in your review.

### Potential Major Issues
1. No sample size justification (CONSORT item 6a)
2. Missing CONSORT flow diagram (item 13a)
3. Reference #22 cannot be verified — possible fabricated reference
4. Table 2 CI inconsistency (CI doesn't contain point estimate)
5. Multiple testing without adjustment (5 secondary outcomes)
6. Discrepancy in follow-up period (12 months vs. 6 months)

### Potential Minor Issues
1. Missing effect sizes for secondary outcomes
2. Reference #15 year discrepancy (2023 in text, 2024 in ref list)
3. Supplementary Table S2 referenced but not provided
4. Limitations section brief
5. Missing CONSORT items (3b, 14b, 17b, 25)
6. Not all secondary outcomes discussed in text

### For Your Expert Judgment
- Is the digital intervention well-described enough for replication?
- Are the outcome measures clinically meaningful?
- Is the comparator appropriate?
- Are the findings generalizable?
```

**Reviewer**: Reviews AI analysis, adds their domain expertise, makes judgment calls on significance:
- Agrees major issues 1-6 are significant
- Adds: intervention description lacks detail for replication
- Notes: the comparator may not reflect current standard of care
- Decision: Recommends **Major Revisions**

9. **Format Final Review** using `templates/reviewer-report-template.md`:

The reviewer edits and finalizes the review based on AI analysis and their own expert assessment.

10. **STOP-05: Reviewer Approves Review** 🛑
    ```
    AWAITING REVIEWER APPROVAL
    Your review addresses 6 major issues and 6 minor issues.
    All findings have been presented as your expert assessment.
    Please review the complete report and confirm before submission.
    ```
    → Reviewer reviews, makes final edits, approves → STOP-05 CLEARED ✅
    → Reviewer submits via journal portal (manual action)

---

## Key Principles Demonstrated

1. **Confidentiality maintained**: No manuscript content sent externally
2. **AI assists, reviewer decides**: AI provides analysis; reviewer makes all judgments
3. **Verification value**: Citation spot-check caught a potentially fabricated reference
4. **Statistical rigor**: GRIM test and consistency checks catch numerical errors
5. **Reporting standards**: CONSORT compliance check identifies missing items
6. **STOP gate respected**: Review submitted only after reviewer approval
