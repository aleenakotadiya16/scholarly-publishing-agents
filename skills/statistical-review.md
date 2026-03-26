# Skill: Statistical Review

## Description

Reviews statistical methods and reporting for completeness, appropriateness, and internal consistency. Checks for common errors, missing elements, suspicious patterns, and compliance with statistical reporting guidelines (SAMPL, EQUATOR).

## When to Use

- During peer review (Workflow 04) — assess statistical quality of submissions
- During manuscript preparation (Workflow 01) — check own statistical reporting
- During integrity screening (Workflow 04) — detect statistical fabrication
- At any point when statistical claims need verification

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `methods_section` | Text | Yes | Statistical methods description |
| `results_section` | Text | Yes | Results text, tables, and figure descriptions |
| `study_type` | Enum | Optional | `rct`, `cohort`, `case_control`, `cross_sectional`, `systematic_review`, `economic_evaluation` |
| `tables` | List | Optional | Structured table data for numerical verification |

## Outputs

| Output | Type | Description |
|---|---|---|
| `completeness_score` | Float 0-100 | Statistical reporting completeness percentage |
| `missing_elements` | List | Required statistical elements not reported |
| `appropriateness_flags` | List | Statistical methods that may be inappropriate |
| `consistency_issues` | List | Internal inconsistencies in reported numbers |
| `integrity_flags` | List | Patterns suggesting fabrication (GRIM/SPRITE failures) |

## Step-by-Step Procedure

### Step 1: Check Reporting Completeness

For each analysis reported, verify the presence of:

| Element | Required? | Notes |
|---|---|---|
| Statistical test named | Yes | Which test was used? |
| Test justification | Recommended | Why this test? (assumptions met?) |
| Alpha level stated | Yes | Usually 0.05, but must be explicit |
| Test statistic value | Yes | t, F, chi-square, z, etc. |
| Degrees of freedom | Yes | For t-tests, ANOVA, chi-square |
| P-value | Yes | Exact values preferred (not just < 0.05) |
| Effect size | Yes (SAMPL) | Cohen's d, OR, RR, HR, etc. |
| Confidence interval | Yes (SAMPL) | 95% CI for primary outcomes |
| Sample size per group | Yes | n for each comparison group |
| Missing data handling | Recommended | How were missing values treated? |
| Multiple comparisons | If applicable | Bonferroni, FDR, etc. |
| Software and version | Recommended | e.g., "Stata 17.0" or "R 4.3.1" |

### Step 2: Check Test Appropriateness

| Data Type | Common Tests | Red Flags |
|---|---|---|
| Continuous, normal | t-test, ANOVA | Using parametric tests on skewed data |
| Continuous, non-normal | Mann-Whitney, Kruskal-Wallis | Using t-test on small non-normal samples |
| Categorical | Chi-square, Fisher's exact | Chi-square with expected cell counts < 5 |
| Time-to-event | Kaplan-Meier, Cox regression | Ignoring non-proportional hazards |
| Repeated measures | Mixed models, GEE | Using independent samples tests on paired data |
| Economic evaluation | ICER, NMB, PSA | Missing uncertainty analysis |

### Step 3: GRIM Test (for integer-based data)

For means derived from integer data (e.g., Likert scales, counts):
```
If N participants each provide an integer value,
then N × mean must be an integer.

Example: Mean = 3.47, N = 20
20 × 3.47 = 69.4 — NOT an integer → GRIM FAIL
```

Apply GRIM test to all reported means where the underlying data is integer-valued.

### Step 4: Internal Consistency Checks

- Do percentages in tables sum to 100% (±1% for rounding)?
- Do subgroup Ns sum to total N?
- Are means/SDs consistent with reported ranges?
- Do reported totals match the sum of components?
- Are degrees of freedom consistent with sample sizes?
- Do confidence intervals contain the point estimate?

### Step 5: P-Value Pattern Analysis

- Are all p-values clustered just below 0.05? (suspicious)
- Is there an appropriate mix of significant and non-significant results?
- Are p-values consistent with test statistics and sample sizes?
- Are exact p-values reported (not just "< 0.05")?

### Step 6: Generate Report

```markdown
## Statistical Review Report

### Reporting Completeness: 78%

#### Present ✅
- Sample sizes reported
- Statistical tests named
- P-values reported (exact values)
- Software identified (R 4.3.1)

#### Missing ⚠️
- Effect sizes not reported for secondary outcomes
- Confidence intervals missing for primary outcome
- Multiple comparisons adjustment not described (5 secondary outcomes tested)
- Missing data handling not described

### Appropriateness Assessment
- Primary analysis (logistic regression): Appropriate ✅
- Sensitivity analysis: Not conducted ⚠️ (recommended for economic evaluations)
- Subgroup analysis: Small sample sizes in subgroups (n=12, 15) — interpret with caution

### Consistency Checks
- Table 2, Column 3: Percentages sum to 102% (likely rounding) ⚠️
- Table 1: N=150 reported in text, but Table 1 shows N=148 ❌

### Integrity Checks
- GRIM test: All means consistent with sample sizes ✅
- P-value distribution: Normal pattern ✅
```

## Quality Criteria

| Criterion | Standard |
|---|---|
| Completeness scoring | All SAMPL-recommended elements checked |
| GRIM accuracy | Correct mathematical verification |
| Consistency checking | All cross-referenceable numbers compared |
| Reporting | Specific locations for all issues cited |

## Cross-References

- Rules: `rules/quality-gates.md` (WARN-02 for incomplete reporting)
- Workflows: `workflows/04-peer-review/integrity-screening.md`
- Agents: Reviewer Agent, Integrity Agent
- Standards: SAMPL guidelines, EQUATOR Network, CONSORT, STROBE
