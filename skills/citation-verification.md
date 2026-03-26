# Skill: Citation Verification

## Description

Verifies that every reference in a manuscript exists and is accurately cited by checking against CrossRef, PubMed, DOI registries, and other scholarly databases. Detects hallucinated citations, blended references, fabricated authors, and nonexistent journals.

## When to Use

- Before submission (mandatory — Workflow 02, STOP-02)
- During literature review (Workflow 01)
- During peer review integrity screening (Workflow 04)
- After revision if new references were added (Workflow 05)
- Final metadata validation (Workflow 06)

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `references` | List of structured references | Yes | Author(s), title, journal, year, volume, issue, pages, DOI |
| `manuscript_text` | Text | Optional | Full manuscript for in-text citation cross-checking |
| `verification_level` | Enum | Optional | `quick` (DOI only), `standard` (DOI + title search), `comprehensive` (all fields) |

## Outputs

| Output | Type | Description |
|---|---|---|
| `verification_report` | Structured report | Status per reference with confidence scores |
| `summary_statistics` | Object | Counts by status (verified, partial, unverified, suspicious, not found) |
| `flagged_references` | List | References requiring human attention |
| `correction_suggestions` | List | Suggested fixes for partially verified references |

## Step-by-Step Procedure

### Step 1: Parse and Structure References

Extract all references into a normalized format:
```json
{
  "ref_id": 1,
  "authors": ["Smith, J.A.", "Jones, B.C."],
  "year": 2024,
  "title": "Full title of the paper",
  "journal": "Journal Name",
  "volume": "12",
  "issue": "3",
  "pages": "45-67",
  "doi": "10.1002/hec.4567"
}
```

### Step 2: DOI Verification (if DOI provided)

```
1. Resolve DOI: GET https://doi.org/{DOI} (follow redirect)
2. Fetch metadata: GET https://api.crossref.org/works/{DOI}
3. Compare: authors, title, journal, year, volume, pages
4. Score: Full match (VERIFIED), partial match (PARTIALLY_VERIFIED), no match (SUSPICIOUS)
```

### Step 3: Title Search (if no DOI or DOI mismatch)

```
1. CrossRef: GET https://api.crossref.org/works?query.title={encoded_title}
2. PubMed: GET https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term={title}[ti]
3. OpenAlex: GET https://api.openalex.org/works?filter=title.search:{title}
4. Evaluate: Exact match → VERIFIED; close match → PARTIALLY_VERIFIED; no match → proceed to Step 4
```

### Step 4: Hallucination Pattern Check

For unverified references, check against known hallucination patterns:
- **Fake authors**: Common name combinations (John Smith, Jane Doe)
- **Blended papers**: Title fragments match multiple different real papers
- **Paraphrased titles**: Close but not exact title matches suggest AI paraphrasing
- **Fake journals**: Journal name doesn't exist in ISSN registry or DOAJ
- **Wrong metadata**: Real paper but wrong year, volume, or author list

### Step 5: Retraction Check

```
1. CrossRef: Check for retraction notices in metadata
2. Retraction Watch: Search for title/DOI in database
3. PubMed: Check for retraction/correction notices
```

### Step 6: Generate Report

Classify each reference and produce the verification report (see `rules/citation-integrity.md` for the full report format).

## Quality Criteria

| Criterion | Threshold |
|---|---|
| Minimum verification rate | 95% VERIFIED |
| Maximum NOT_FOUND tolerance | 0% (all must be resolved) |
| Maximum SUSPICIOUS tolerance | 0% (all must be human-reviewed) |
| PARTIALLY_VERIFIED | Must be corrected before submission |
| Processing time target | < 2 seconds per reference (API-dependent) |

## Cross-References

- Rules: `rules/citation-integrity.md` (comprehensive citation rules)
- Workflows: `workflows/02-pre-submission/reference-validation.md`
- Agents: Author Agent, Integrity Agent
- Config: `config/quality-thresholds.yaml` (verification thresholds)
