# Journal Selection

## Purpose

Help authors identify the most appropriate journals for their manuscript based on evidence-based criteria including scope alignment, impact metrics, open access policy, turnaround time, and acceptance rate.

---

## Selection Criteria

### 1. Scope Alignment (Weight: 35%)

- Does the journal publish in this discipline/subdiscipline?
- Does the journal publish this type of article (original research, review, case study)?
- Does the journal's stated scope match the manuscript's topic?
- Has the journal published similar work recently?

### 2. Impact and Visibility (Weight: 20%)

| Metric | Source | Considerations |
|---|---|---|
| Journal Impact Factor (JIF) | Clarivate Journal Citation Reports | Traditional measure; field-specific norms |
| CiteScore | Scopus | Alternative to JIF; broader citation window |
| h-index | Scopus, Google Scholar | Journal-level productivity/impact |
| Indexing | PubMed, Scopus, Web of Science | Critical for discoverability |
| Altmetric attention | Altmetric | Social/media impact potential |

### 3. Open Access Policy (Weight: 15%)

| Model | Description | Considerations |
|---|---|---|
| Full OA (Gold) | All articles freely accessible; APC required | Funder mandates, budget |
| Hybrid | Subscription journal with OA option; APC for OA articles | Higher APCs, transformative agreements |
| Subscription | Behind paywall unless author pays APC | No cost to author, limited access |
| Green OA | Preprint/postprint self-archiving allowed | Check embargo period |
| Diamond/Platinum OA | Free to read and publish | Uncommon in medicine; check quality |

Check funder requirements — many funders (NHMRC, Wellcome Trust, NIH, UKRI) mandate open access.

### 4. Turnaround Time (Weight: 15%)

| Stage | Typical Range | Fast Journals |
|---|---|---|
| Initial decision | 1-4 weeks | Some journals offer rapid review |
| Peer review | 4-12 weeks | Fast-track journals: 2-4 weeks |
| Revision → decision | 2-4 weeks | |
| Acceptance → publication | 1-4 weeks (online first) | Some journals: days |

Sources: Journal websites, Publons, author experience databases, AcademicKarma.

### 5. Acceptance Rate (Weight: 10%)

- High-impact journals: 5-15% acceptance rate
- Mid-tier journals: 20-40%
- Specialized journals: 30-60%
- Consider the manuscript's strength honestly; targeting too high wastes time

### 6. Practical Considerations (Weight: 5%)

- Page charges / APCs / color figure charges
- Formatting requirements (some journals require specific LaTeX templates)
- Open data requirements
- Cover letter requirements
- Suggested reviewer requirements
- Preprint policy (does the journal allow preprints?)

---

## Journal Selection Procedure

### Step 1: Manuscript Profile

Extract key attributes:
```yaml
manuscript_profile:
  discipline: "Health Economics"
  subdiscipline: "Cost-effectiveness analysis"
  article_type: "Original Research"
  keywords: ["telehealth", "cost-effectiveness", "rural health", "economic evaluation"]
  methodology: "Decision-analytic model with probabilistic sensitivity analysis"
  population: "Rural populations in Australia"
  word_count: 3500
  figure_count: 4
  table_count: 3
  reference_count: 45
```

### Step 2: Query Journal Database

Use `config/journal-requirements.yaml` plus external sources:
1. Match keywords and discipline to journal scope statements
2. Filter by article type acceptance
3. Filter by practical constraints (OA requirements, budget)

### Step 3: Rank and Present

Present a ranked list with rationale:

```markdown
## Recommended Journals

### 1. Health Economics (Wiley) — Fit Score: 92%
- **Scope match**: Core health economics journal; regularly publishes CEA
- **Impact**: JIF 3.2; CiteScore 5.1; PubMed indexed
- **OA**: Hybrid (APC ~$4,200 for OA option)
- **Turnaround**: ~8 weeks to first decision
- **Acceptance rate**: ~25%
- **Notes**: Strong fit for methodology; check recent issues for similar topics

### 2. Value in Health (Elsevier) — Fit Score: 88%
- **Scope match**: ISPOR journal; excellent for economic evaluations
- **Impact**: JIF 5.7; CiteScore 8.3; PubMed indexed
- **OA**: Hybrid (APC ~$3,500 for OA option)
- **Turnaround**: ~10 weeks to first decision
- **Acceptance rate**: ~20%
- **Notes**: Higher impact but more competitive; consider if results are strong

### 3. BMC Health Services Research (Springer Nature) — Fit Score: 82%
- **Scope match**: Broad health services scope; publishes economic evaluations
- **Impact**: JIF 2.4; CiteScore 4.0; PubMed indexed
- **OA**: Full OA (APC ~$2,490)
- **Turnaround**: ~6 weeks to first decision
- **Acceptance rate**: ~40%
- **Notes**: Good backup option; faster turnaround; NHMRC compliant OA
```

### Step 4: Author Decision

The author selects the target journal. The agent does NOT make this decision. Factors the author should consider:
- Career stage (early career may benefit from mid-tier journals with faster turnaround)
- Funding timelines (grants may have reporting deadlines)
- Funder OA mandates
- Audience (who needs to see this work?)

---

## Predatory Journal Warning

If any journal in the results matches predatory indicators, trigger WARN-05:

- Not indexed in PubMed, Scopus, or Web of Science
- No clear editorial board or board members from unrelated fields
- Aggressive solicitation emails
- Very rapid peer review promises (< 1 week)
- No clear retraction policy
- Listed on Beall's List or Cabell's Predatory Reports

---

## Cascading Strategy

Help the author plan a cascading submission strategy (if first-choice journal rejects):

```
Journal 1 (ambitious): Nature Medicine → if rejected →
Journal 2 (realistic): Health Economics → if rejected →
Journal 3 (backup): BMC Health Services Research
```

For each cascade level, note what reformatting would be needed.
