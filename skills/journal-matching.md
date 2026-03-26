# Skill: Journal Matching

## Description

Matches a manuscript to suitable target journals based on scope alignment, impact factor, open access policy, turnaround time, acceptance rate, and author preferences. Produces a ranked recommendation list with evidence-based rationale.

## When to Use

- During submission planning (Workflow 03)
- When an author asks "which journal should I submit to?"
- After a rejection, to identify the next target journal
- When planning a cascading submission strategy

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `abstract` | Text | Yes | Manuscript abstract |
| `keywords` | List | Yes | Manuscript keywords / MeSH terms |
| `discipline` | String | Yes | Primary discipline (e.g., "health economics") |
| `article_type` | Enum | Yes | `original_research`, `review`, `case_study`, `letter`, `systematic_review` |
| `author_preferences` | Object | Optional | OA requirement, speed priority, prestige priority, budget constraints |
| `previous_submissions` | List | Optional | Journals already submitted to (to exclude) |
| `funder_requirements` | Object | Optional | OA mandates, specific compliance requirements |

## Outputs

| Output | Type | Description |
|---|---|---|
| `recommendations` | Ranked list | Top 5-10 journals with fit scores and rationale |
| `cascade_strategy` | List | Ordered submission plan (ambitious → realistic → backup) |
| `warnings` | List | Potential predatory journals flagged, funder compliance issues |

## Step-by-Step Procedure

### Step 1: Build Manuscript Profile

```yaml
profile:
  discipline: "Health Economics"
  subdiscipline: "Cost-effectiveness analysis"
  keywords: ["telehealth", "cost-effectiveness", "rural health"]
  methodology: "Decision-analytic model"
  article_type: "original_research"
  word_count: 3500
  novelty_level: "moderate"  # self-assessed
```

### Step 2: Query Journal Database

1. Check `config/journal-requirements.yaml` for pre-configured journals
2. Match keywords against journal scope statements
3. Filter by article type, methodology fit, and practical constraints
4. Score each journal across all criteria

### Step 3: Calculate Fit Scores

Weighted scoring (adjust weights based on author preferences):

| Criterion | Default Weight | Scoring Method |
|---|---|---|
| Scope alignment | 35% | Keyword match, recent publication analysis |
| Impact/visibility | 20% | JIF, CiteScore, indexing status |
| OA policy | 15% | Match with funder mandates, author preference |
| Turnaround time | 15% | Average time to first decision |
| Acceptance rate | 10% | Realistic assessment of manuscript competitiveness |
| Practical factors | 5% | APC cost, formatting burden, preprint policy |

### Step 4: Predatory Journal Screen

For each recommended journal, verify:
- Indexed in PubMed, Scopus, or Web of Science
- Clear editorial board with verifiable members
- Transparent peer review process described
- Not on Beall's List or Cabell's Predatory Reports
- Published by a recognized publisher or academic institution

If predatory indicators detected → WARN-05.

### Step 5: Funder Compliance Check

If author has funder requirements:
- NHMRC: Requires OA within 12 months
- NIH: Requires PubMed Central deposit
- Wellcome Trust: Requires immediate OA (CC-BY)
- UKRI: Requires immediate OA for peer-reviewed articles
- ARC: Requires OA within 12 months

### Step 6: Generate Recommendations

Present ranked list with full rationale for each recommendation. Include a cascading strategy from ambitious to realistic to backup options.

## Quality Criteria

| Criterion | Standard |
|---|---|
| Scope accuracy | Journal genuinely publishes in the matched area |
| Metric currency | Impact factors from most recent available year |
| Policy accuracy | OA and disclosure policies verified against current guidelines |
| Practical value | Recommendations actionable (not just "submit to Nature") |

## Cross-References

- Config: `config/journal-requirements.yaml`
- Workflows: `workflows/03-submission/journal-selection.md`
- Agents: Author Agent
- Rules: `rules/quality-gates.md` (WARN-05 for predatory journals)
