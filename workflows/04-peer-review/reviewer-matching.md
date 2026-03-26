# Reviewer Matching

## Purpose

Assist editors in identifying appropriate peer reviewers based on expertise, publication history, availability, and conflict-of-interest screening.

---

## Matching Criteria

### 1. Expertise Match (Weight: 40%)

| Method | Description |
|---|---|
| **Keyword matching** | Match manuscript keywords against potential reviewer expertise |
| **Publication history** | Find researchers who have published on similar topics |
| **Citation analysis** | Authors of papers cited in the manuscript (who are not co-authors) |
| **MeSH term matching** | For biomedical papers, match MeSH terms |
| **Methodological expertise** | Match specific methods (meta-analysis, RCT, qualitative, etc.) |

### 2. Availability and Activity (Weight: 20%)

| Factor | Consideration |
|---|---|
| **Recent publications** | Active researchers (published within last 2 years) |
| **Review history** | Has reviewed for this or similar journals before |
| **Current workload** | Not already reviewing multiple papers for this journal |
| **Response time** | Historical response rate and timeliness |
| **Career stage** | Mix of senior and early-career reviewers |

### 3. Conflict of Interest Screening (Weight: 25%)

**Automatic disqualification**:
- Co-authored with any manuscript author (past 3-5 years)
- Same institution or department as any author
- Known advisor-advisee relationship
- Financial relationship (shared grants, consulting)
- Involved in competing research

**Detection methods**:
1. Search PubMed/CrossRef for co-authored publications
2. Check institutional affiliations
3. Analyze co-citation networks
4. Cross-reference funding databases (where accessible)
5. Check editorial board membership (potential power dynamic)

### 4. Diversity Considerations (Weight: 15%)

- **Geographic diversity**: Reviewers from different countries/regions
- **Institutional diversity**: Different universities/research groups
- **Career stage diversity**: Mix of established and emerging voices
- **Perspective diversity**: Different methodological approaches or viewpoints
- **Gender balance**: Aim for balanced reviewer panels where possible

---

## Matching Procedure

### Step 1: Extract Manuscript Profile
```yaml
manuscript_profile:
  topic: "Cost-effectiveness of telehealth in rural settings"
  keywords: ["health economics", "telehealth", "cost-effectiveness", "rural health"]
  methods: ["decision-analytic model", "probabilistic sensitivity analysis", "ICER calculation"]
  mesh_terms: ["Telemedicine", "Cost-Benefit Analysis", "Rural Health Services"]
  authors:
    - name: "Mordaunt, D.A."
      institution: "Flinders University"
      orcid: "0000-0000-0000-0000"
  cited_authors: ["Author1", "Author2", "Author3"]
```

### Step 2: Search for Candidate Reviewers

1. **PubMed author search**: Find researchers publishing on similar topics
2. **CrossRef reverse citation**: Authors who cited similar work
3. **Journal reviewer database**: Previous reviewers with matching expertise
4. **ORCID search**: Researchers with matching keywords in their profile
5. **Editorial board**: Board members with relevant expertise (if not conflicted)

### Step 3: Screen for Conflicts

For each candidate:
```markdown
### Candidate: Dr. Jane Smith, University of Melbourne
- **Expertise match**: 85% (published 3 papers on telehealth cost-effectiveness)
- **Availability**: Active (2 papers in 2025)
- **COI screen**:
  - Co-authorship with manuscript authors: ❌ None found
  - Same institution: ❌ Different institution
  - Shared grants: ❌ None found
  - Competing research: ⚠️ Has a similar study in progress (check with editor)
- **Review history**: Reviewed 2 papers for this journal in past year
- **Recommendation**: Suitable (pending editor check on competing research)
```

### Step 4: Present Ranked List

```markdown
## Suggested Reviewers

### Tier 1: Strong Match (recommend inviting)
1. Dr. Jane Smith, University of Melbourne (expertise: 85%, no COI)
2. Dr. Robert Chen, University of Toronto (expertise: 82%, no COI)
3. Prof. Maria Garcia, London School of Economics (expertise: 78%, no COI)

### Tier 2: Good Match (backup options)
4. Dr. Yuki Tanaka, University of Tokyo (expertise: 75%, no COI)
5. Dr. Sarah Williams, Harvard T.H. Chan School (expertise: 72%, no COI)

### Excluded (COI detected)
- Dr. Alex Brown, Flinders University (same institution as corresponding author)
- Dr. Wei Liu, University of Queensland (co-authored with Author 1 in 2024)

### Notes
- All candidates verified against CrossRef for co-authorship
- Geographic diversity: Australia, Canada, UK, Japan, USA
- Mix of career stages: 2 professors, 2 associate professors, 1 senior lecturer
```

---

## Invitation Support

For each invited reviewer, the editor can send:
- Manuscript title and abstract
- Estimated review timeline
- Journal review guidelines
- Structured review template (see `templates/reviewer-report-template.md`)
- Reminder about confidentiality requirements

---

## Handling Declined Invitations

If reviewers decline:
1. Move to Tier 2 candidates
2. If all decline, expand search criteria (broader keywords, different databases)
3. Consider: Is the topic too niche? Should the search strategy be adjusted?
4. Track decline reasons (too busy, out of scope, COI) for future matching improvement
