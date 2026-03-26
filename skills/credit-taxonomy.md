# Skill: CRediT Taxonomy

## Description

Assists in assigning CRediT (Contributor Roles Taxonomy) roles to manuscript authors. Maps each author's contributions to the 14 standardized CRediT roles and generates formatted contribution statements.

## When to Use

- During metadata preparation (Workflow 02)
- When preparing a new manuscript with multiple authors
- When responding to journal requests for author contributions
- When verifying authorship compliance with ICMJE criteria

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `authors` | List | Yes | Author names in order |
| `contributions` | Object | Yes | Free-text description of what each author did |
| `authorship_level` | Enum | Optional | `lead` / `equal` / `supporting` per author |

## Outputs

| Output | Type | Description |
|---|---|---|
| `role_assignments` | Matrix | Author × Role matrix with assignments |
| `formatted_statement` | Text | Ready-to-insert contribution statement |
| `validation_flags` | List | Issues (unassigned roles, authors without roles, ICMJE concerns) |

## The 14 CRediT Roles

| # | Role | Definition |
|---|---|---|
| 1 | **Conceptualization** | Ideas; formulation of research goals and aims |
| 2 | **Data curation** | Management activities to annotate, scrub, maintain data |
| 3 | **Formal analysis** | Application of statistical, mathematical, computational techniques |
| 4 | **Funding acquisition** | Acquisition of the financial support for the project |
| 5 | **Investigation** | Conducting research and investigation; performing experiments, data collection |
| 6 | **Methodology** | Development or design of methodology; creation of models |
| 7 | **Project administration** | Management and coordination responsibility for the research activity |
| 8 | **Resources** | Provision of study materials, reagents, patients, laboratory samples, computing resources |
| 9 | **Software** | Programming, software development; designing computer programs |
| 10 | **Supervision** | Oversight and leadership responsibility for the research activity |
| 11 | **Validation** | Verification of the overall replication/reproducibility of results |
| 12 | **Visualization** | Preparation, creation and/or presentation of data visualizations |
| 13 | **Writing – original draft** | Preparation of the initial draft |
| 14 | **Writing – review & editing** | Critical review, commentary, or revision of the draft |

## Step-by-Step Procedure

### Step 1: Gather Contribution Information

For each author, ask what they did:
```
Author 1 (Dylan Mordaunt): Designed the study, supervised the team,
  obtained funding, wrote the first draft, reviewed all revisions
Author 2 (Jane Smith): Conducted the analysis, created figures,
  helped with methodology, reviewed the manuscript
Author 3 (Bob Jones): Collected data, managed the database,
  reviewed the manuscript
```

### Step 2: Map to CRediT Roles

Create an author-role matrix:

| Role | Dylan Mordaunt | Jane Smith | Bob Jones |
|---|---|---|---|
| Conceptualization | ✅ | | |
| Data curation | | | ✅ |
| Formal analysis | | ✅ | |
| Funding acquisition | ✅ | | |
| Investigation | | | ✅ |
| Methodology | ✅ | ✅ | |
| Project administration | ✅ | | |
| Resources | ✅ | | |
| Software | | ✅ | |
| Supervision | ✅ | | |
| Validation | | ✅ | |
| Visualization | | ✅ | |
| Writing – original draft | ✅ | | |
| Writing – review & editing | ✅ | ✅ | ✅ |

### Step 3: Validate Assignments

Check for issues:
- [ ] Every author has at least one role (ICMJE compliance)
- [ ] Every author has "Writing – review & editing" OR explicit approval documented
- [ ] Critical roles are assigned (Conceptualization, Formal analysis, Writing)
- [ ] No CRediT roles are unassigned (WARN-07 if gaps exist)
- [ ] Roles reflect ICMJE authorship criteria (substantial contribution required)

### Step 4: Generate Formatted Statement

```
Author contributions: DAM: Conceptualization, Funding acquisition,
Methodology, Project administration, Resources, Supervision,
Writing – original draft, Writing – review & editing. JS: Formal analysis,
Methodology, Software, Validation, Visualization, Writing – review & editing.
BJ: Data curation, Investigation, Writing – review & editing.
```

### Step 5: ICMJE Cross-Check

Verify each listed author meets ALL FOUR ICMJE criteria:
1. Substantial contributions to conception/design OR data acquisition/analysis
2. Drafting the work OR revising it critically
3. Final approval of the version to be published
4. Agreement to be accountable for all aspects of the work

## Quality Criteria

| Criterion | Standard |
|---|---|
| Completeness | All 14 roles considered for assignment |
| Accuracy | Roles reflect actual contributions |
| ICMJE compliance | All authors meet all 4 criteria |
| No orphan roles | Critical roles have at least one assignee |

## Cross-References

- Workflows: `workflows/02-pre-submission/metadata-preparation.md`
- Agents: Author Agent
- Standards: CRediT (NISO Z39.104), ICMJE authorship criteria
- Config: JATS-XML CRediT encoding in `skills/jats-xml-conversion.md`
