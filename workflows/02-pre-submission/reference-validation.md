# Reference Validation

## Purpose

Systematically validate every reference in the manuscript before submission. This is a STOP gate (STOP-02) — all flagged references must be resolved before the workflow can proceed.

---

## Validation Procedure

### Step 1: Extract References

Parse the manuscript to create a structured reference list:

```json
{
  "references": [
    {
      "ref_number": 1,
      "authors": ["Smith, J.A.", "Jones, B.C."],
      "year": 2024,
      "title": "Cost-effectiveness of telehealth in rural settings",
      "journal": "Health Economics",
      "volume": "33",
      "issue": "5",
      "pages": "1120-1135",
      "doi": "10.1002/hec.4567",
      "in_text_locations": ["Introduction para 2", "Discussion para 4"]
    }
  ]
}
```

### Step 2: DOI-Based Verification

For references with DOIs:
1. Resolve DOI via `https://doi.org/{DOI}`
2. Fetch metadata from CrossRef API: `https://api.crossref.org/works/{DOI}`
3. Compare returned metadata against cited metadata
4. Flag any discrepancies (wrong author, wrong year, wrong title, etc.)

### Step 3: Title-Based Search

For references without DOIs (or where DOI doesn't match):
1. Search CrossRef by title: `https://api.crossref.org/works?query.title={title}`
2. Search PubMed by title: E-utilities API
3. Search OpenAlex by title
4. Evaluate match quality (exact match, close match, no match)

### Step 4: Author Verification

For each reference:
1. Verify authors have published in the cited field
2. Check for common hallucination patterns (see `rules/citation-integrity.md`)
3. Cross-reference with ORCID if available
4. Flag suspicious author combinations

### Step 5: Journal Verification

For each unique journal:
1. Verify journal exists (ISSN lookup)
2. Check indexing status (PubMed, Scopus, Web of Science)
3. Check for predatory indicators
4. Verify the specific volume/issue/year combination exists

### Step 6: In-Text Citation Consistency

1. Every in-text citation must have a corresponding reference list entry
2. Every reference list entry must be cited in the text
3. Citation numbers must be sequential (for numbered styles)
4. Author-year citations must match the reference list exactly

### Step 7: Retraction Check

For all references:
1. Check against Retraction Watch database
2. Check CrossRef metadata for retraction notices
3. Check PubMed for retraction/correction notices
4. Flag any retracted papers

---

## Verification Report Format

```markdown
## Reference Validation Report
Date: [DATE]
Manuscript: [TITLE]
Total references: [N]

### Summary
| Status | Count | Percentage |
|---|---|---|
| VERIFIED | X | X% |
| PARTIALLY_VERIFIED | X | X% |
| UNVERIFIED | X | X% |
| SUSPICIOUS | X | X% |
| NOT_FOUND | X | X% |
| RETRACTED | X | X% |

### Detailed Findings

#### VERIFIED References
[List of verified references — no action needed]

#### PARTIALLY_VERIFIED References
[List with specific discrepancies and recommended corrections]

#### UNVERIFIED References
[List with verification attempts made and results]

#### SUSPICIOUS References
[List with specific concerns — hallucination pattern matches]

#### NOT_FOUND References
[List of references that could not be found in any database]

#### RETRACTED References
[List of retracted papers with retraction notice details]
```

---

## Resolution Requirements (STOP-02)

Before clearing STOP-02, the author must:

1. **VERIFIED**: No action needed
2. **PARTIALLY_VERIFIED**: Correct discrepancies (fix author names, years, DOIs, etc.)
3. **UNVERIFIED**: Either provide evidence the reference exists or remove it
4. **SUSPICIOUS**: Verify manually (retrieve the actual paper) or remove
5. **NOT_FOUND**: Remove from manuscript and replace with a verified alternative
6. **RETRACTED**: Remove and replace (unless citing the retraction itself is relevant)

**Zero tolerance**: No SUSPICIOUS, NOT_FOUND, or RETRACTED references may remain in the final manuscript (unless the retraction itself is the subject of discussion).

---

## API Rate Limits and Best Practices

| API | Rate Limit | Best Practice |
|---|---|---|
| CrossRef | Polite pool: 50 req/sec with `mailto` | Include contact email in requests |
| PubMed E-utilities | 3 req/sec (without API key), 10 req/sec (with key) | Batch queries where possible |
| OpenAlex | 100,000 req/day | Use pagination for large result sets |
| Semantic Scholar | 100 req/5 min (unauthenticated) | Use API key for higher limits |
