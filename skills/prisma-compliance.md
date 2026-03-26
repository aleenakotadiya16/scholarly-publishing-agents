# Skill: PRISMA Compliance

## Description

Checks systematic review and scoping review manuscripts against PRISMA 2020 (or PRISMA-ScR for scoping reviews) reporting guidelines. Identifies missing items and provides specific recommendations for improvement.

## When to Use

- During manuscript preparation of systematic reviews (Workflow 01)
- During pre-submission check (Workflow 02)
- During peer review of systematic reviews (Workflow 04)
- When WARN-09 is triggered

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `manuscript` | Text | Yes | Full systematic review manuscript |
| `prisma_variant` | Enum | Yes | `prisma_2020`, `prisma_scr`, `prisma_p`, `prisma_s`, `prisma_dta` |
| `protocol_registration` | Object | Optional | PROSPERO or OSF registration details |
| `flow_diagram` | Boolean | Optional | Whether a PRISMA flow diagram is included |

## Outputs

| Output | Type | Description |
|---|---|---|
| `compliance_score` | Float 0-100 | Percentage of applicable items reported |
| `item_checklist` | List | Status per PRISMA item (reported / partial / missing / NA) |
| `missing_items` | List | Items not reported with specific recommendations |
| `flow_diagram_check` | Object | Whether flow diagram is present and complete |

## PRISMA 2020 Checklist (27 items)

| # | Section | Item | Key Requirements |
|---|---|---|---|
| 1 | Title | Title | Identify as systematic review, meta-analysis, or both |
| 2 | Abstract | Abstract | Structured summary including PICO, methods, results, conclusion |
| 3 | Introduction | Rationale | Describe rationale in context of existing knowledge |
| 4 | Introduction | Objectives | Explicit statement of question(s) using PICO |
| 5 | Methods | Eligibility criteria | Inclusion/exclusion criteria with rationale |
| 6 | Methods | Information sources | Databases, registries, websites, contacts, reference lists |
| 7 | Methods | Search strategy | Full search strategy for at least one database |
| 8 | Methods | Selection process | Screening process, number of screeners, arbitration |
| 9 | Methods | Data collection | Data extraction process, number of extractors, arbitration |
| 10 | Methods | Data items | List of all variables sought, assumptions about missing data |
| 11 | Methods | Study risk of bias | Methods for assessing bias (e.g., RoB 2, ROBINS-I) |
| 12 | Methods | Effect measures | Specify effect measures (OR, RR, MD, etc.) |
| 13 | Methods | Synthesis methods | Criteria for meta-analysis, methods for combining results |
| 14 | Methods | Reporting bias | Methods for assessing publication bias |
| 15 | Methods | Certainty assessment | Methods for assessing certainty (e.g., GRADE) |
| 16 | Results | Study selection | Flow diagram with numbers at each stage |
| 17 | Results | Study characteristics | Characteristics of included studies |
| 18 | Results | Risk of bias in studies | Bias assessment results per study |
| 19 | Results | Individual results | Results per study (forest plots if meta-analysis) |
| 20 | Results | Synthesis results | Results of synthesis (pooled estimates, heterogeneity) |
| 21 | Results | Reporting biases | Results of reporting bias assessment |
| 22 | Results | Certainty of evidence | GRADE or equivalent assessment per outcome |
| 23 | Discussion | Discussion | Interpretation in context, limitations, implications |
| 24 | Other | Registration/protocol | Registration number, protocol accessibility |
| 25 | Other | Support | Funding sources, role of funders |
| 26 | Other | Competing interests | Declarations |
| 27 | Other | Data/code availability | Availability of data, code, materials |

## Step-by-Step Procedure

### Step 1: Identify PRISMA Variant

- **PRISMA 2020**: Standard systematic reviews and meta-analyses
- **PRISMA-ScR**: Scoping reviews (modified checklist)
- **PRISMA-P**: Protocols for systematic reviews
- **PRISMA-S**: Search reporting extension
- **PRISMA-DTA**: Diagnostic test accuracy

### Step 2: Scan Manuscript Section by Section

For each PRISMA item:
1. Identify the manuscript section where it should appear
2. Search for the relevant content
3. Classify: `reported` / `partially_reported` / `not_reported` / `not_applicable`
4. For partial reports, note what's missing

### Step 3: Check Flow Diagram

The PRISMA flow diagram is a critical requirement:
- [ ] Flow diagram present
- [ ] Number of records identified from each source
- [ ] Number after duplicate removal
- [ ] Number screened (title/abstract)
- [ ] Number excluded at screening (with reasons)
- [ ] Number assessed for eligibility (full text)
- [ ] Number excluded at full text (with reasons by category)
- [ ] Number included in qualitative synthesis
- [ ] Number included in quantitative synthesis (meta-analysis)

### Step 4: Check Registration

- [ ] Protocol registered (PROSPERO, OSF, or other)
- [ ] Registration number provided in manuscript
- [ ] Protocol deviations described if any

### Step 5: Generate Report

```markdown
## PRISMA 2020 Compliance Report

### Overall Compliance: 81% (22/27 items fully reported)

### Summary
| Status | Count |
|---|---|
| Fully reported | 22 |
| Partially reported | 3 |
| Not reported | 2 |
| Not applicable | 0 |

### Missing Items

#### Item 14: Reporting Bias Assessment — NOT REPORTED
- **What's needed**: Methods used to assess publication bias (e.g., funnel plot, Egger's test)
- **Where to add**: Methods section, subsection on synthesis methods
- **Recommendation**: Describe the method used to assess publication bias, or state that it was not assessed with rationale

#### Item 22: Certainty of Evidence — NOT REPORTED
- **What's needed**: GRADE or equivalent assessment for each primary outcome
- **Where to add**: Results section, after synthesis results
- **Recommendation**: Add a GRADE evidence profile table

#### Item 7: Search Strategy — PARTIALLY REPORTED
- **What's missing**: Full search strategy provided for PubMed but not for Embase or Cochrane
- **Recommendation**: Include the complete search string for all databases searched
```

## Quality Criteria

| Criterion | Standard |
|---|---|
| Item identification accuracy | Correctly identifies presence/absence of each PRISMA item |
| Specificity | Provides exact locations and specific missing content |
| Recommendations | Actionable, with clear instructions for addressing gaps |
| Variant awareness | Correctly applies the appropriate PRISMA variant |

## Cross-References

- Workflows: `workflows/01-manuscript-preparation/formatting-compliance.md`
- Agents: Author Agent, Reviewer Agent
- Rules: `rules/quality-gates.md` (WARN-09 for non-compliance)
- Standards: PRISMA 2020, PRISMA-ScR, EQUATOR Network
- Tools: ASReview (for AI-assisted screening)
