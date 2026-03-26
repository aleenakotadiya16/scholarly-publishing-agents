# Citation Integrity Rules

## Why This Matters

Citation integrity is the single highest-risk area for AI-assisted scholarly publishing. Large language models hallucinate citations at alarming rates:

- **NeurIPS 2025**: GPTZero identified 100+ hallucinated citations across 53 papers submitted to NeurIPS (Fortune, January 2026). These were not random errors — they were plausible-looking references that passed casual review.
- **Deakin University study**: Researchers found that ChatGPT fabricated approximately 20% of academic citations when asked to generate reference lists.
- **Systematic patterns**: AI models blend real papers, invent author names (often defaulting to common names like "Smith" or "Zhang"), paraphrase real titles into fake ones, and create references to nonexistent journals or conferences.

**Every single citation in a manuscript must be independently verified.** This is not optional.

---

## Verification Rules

### Rule 1: Never Generate Citations from Memory

AI models should NEVER produce citations based on their training data alone. Training data is:
- Incomplete (not all papers are in training data)
- Potentially corrupted (AI-on-AI feedback loops)
- Blended (model may merge multiple papers into one fabricated reference)

**Correct approach**: Use external verification services (CrossRef, PubMed, DOI resolution) to confirm every reference.

### Rule 2: Verify Against Authoritative Sources

Every citation must be checked against at least one of:

| Source | API | What It Verifies |
|---|---|---|
| **CrossRef** | `https://api.crossref.org/works/{DOI}` | DOI existence, metadata accuracy, title, authors, journal |
| **PubMed/NCBI** | `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/` | PMID existence, biomedical article metadata |
| **DOI Resolution** | `https://doi.org/{DOI}` | DOI resolves to the correct article |
| **OpenAlex** | `https://api.openalex.org/works` | Open database of scholarly works |
| **Semantic Scholar** | `https://api.semanticscholar.org/v1/paper/{id}` | Paper existence and metadata |

### Rule 3: Check All Citation Components

For each reference, verify:

1. **Authors**: Do these authors exist? Have they published in this field? Are the names spelled correctly?
2. **Title**: Does this exact title exist? (Watch for AI-paraphrased titles)
3. **Journal/Conference**: Is this a real, active journal? (Watch for AI-invented journal names)
4. **Year**: Does the publication year match the actual publication?
5. **Volume/Issue/Pages**: Do these match the real article?
6. **DOI**: Does the DOI resolve to the correct article?

### Rule 4: Flag Unverifiable References

If a reference cannot be verified, it must be flagged — not silently dropped or replaced. Use this classification:

| Status | Meaning | Action |
|---|---|---|
| `VERIFIED` | All components confirmed against external source | No action needed |
| `PARTIALLY_VERIFIED` | Some components match but not all | Flag for human review |
| `UNVERIFIED` | Cannot confirm existence via any source | Mark `[UNVERIFIED]`, require human action |
| `SUSPICIOUS` | Matches hallucination patterns | Mark `[SUSPICIOUS]`, escalate to Integrity Agent |
| `NOT_FOUND` | No matching record in any database | Mark `[NOT FOUND]`, likely fabricated |

---

## Hallucination Detection Patterns

### Pattern 1: Fake Authors

AI models often generate plausible-sounding but nonexistent author combinations:

- **Common name defaults**: "John Smith", "Jane Doe", "J. Wang", "S. Kumar" — if an author name is very common and the paper can't be found, this is suspicious.
- **Author-field mismatch**: An author known for molecular biology cited for a health economics paper they never wrote.
- **Name blending**: Real first name from one author + real last name from another.

**Detection**: Cross-reference author names with ORCID, PubMed author search, and institutional pages.

### Pattern 2: Blended Papers

AI merges elements from two or more real papers into one fabricated reference:

- Real author from Paper A + real title fragment from Paper B + real journal from Paper C
- The resulting reference looks plausible but doesn't exist as a single work.

**Detection**: Search for the exact title. If the title returns no results but individual words return related (but different) papers, this is likely a blended citation.

### Pattern 3: Paraphrased Titles

AI takes a real paper title and slightly rephrases it:

- Real: "Effect of metformin on cardiovascular outcomes in type 2 diabetes"
- Hallucinated: "Impact of metformin therapy on cardiovascular events among patients with type 2 diabetes mellitus"

**Detection**: Search for the exact title in quotes. If no match, search for key phrases. If a similar (but different) paper is found, this is likely a paraphrased hallucination.

### Pattern 4: Nonexistent Journals

AI invents journal names that sound real:

- "Journal of Advanced Medical Research" (doesn't exist)
- "International Review of Health Economics and Policy" (doesn't exist)
- Blends of real journal names: "The Lancet Global Health Economics" (not real)

**Detection**: Verify journal names against Ulrich's Periodical Directory, DOAJ, or the publisher's website.

### Pattern 5: Wrong Year/Volume

AI assigns the wrong publication year or volume number to a real paper:

- The paper exists but was published in 2019, not 2021 as cited.
- The volume number doesn't match the year.

**Detection**: Cross-reference DOI metadata for exact publication date and volume.

### Pattern 6: Retracted Papers

AI may cite papers that have been retracted, as training data may predate retraction:

**Detection**: Check Retraction Watch database and CrossRef retraction metadata.

---

## Verification Procedure

### Step 1: Extract Reference List

Parse the manuscript to extract all cited references into a structured format:
```
{
  "authors": ["Last, F.", "Last, F."],
  "year": "2024",
  "title": "Full title of the paper",
  "journal": "Journal Name",
  "volume": "12",
  "issue": "3",
  "pages": "45-67",
  "doi": "10.xxxx/xxxxx"
}
```

### Step 2: DOI-First Verification

If a DOI is provided:
1. Resolve the DOI via `https://doi.org/{DOI}`
2. Fetch metadata from CrossRef API
3. Compare all fields (authors, title, journal, year) against the cited reference
4. Flag any discrepancies

### Step 3: Title Search

If no DOI or DOI doesn't match:
1. Search CrossRef by exact title
2. Search PubMed by exact title
3. Search OpenAlex by exact title
4. If no exact match, search by key phrases to detect paraphrased titles

### Step 4: Author Verification

For each author:
1. Search PubMed for author's publication history
2. Check ORCID for author profile
3. Verify the author has published in the cited field
4. Flag authors who appear fabricated

### Step 5: Journal Verification

For each journal:
1. Verify the journal exists (ISSN lookup, publisher website)
2. Check if the journal is indexed (PubMed, Scopus, Web of Science)
3. Check for predatory journal indicators (Beall's List, DOAJ verification)
4. Verify the volume/issue/year combination is plausible

### Step 6: Generate Report

Produce a verification report:
```markdown
## Citation Verification Report

Total references: 45
- VERIFIED: 38 (84.4%)
- PARTIALLY_VERIFIED: 4 (8.9%)
- UNVERIFIED: 2 (4.4%)
- SUSPICIOUS: 1 (2.2%)
- NOT_FOUND: 0

### Flagged References

#### Reference #12 — SUSPICIOUS
- Cited: Smith, J., & Doe, J. (2023). "Impact of AI on systematic reviews." Journal of Medical Informatics, 15(2), 112-125.
- Issue: Title not found in CrossRef. Similar paper by different authors exists. Author names are common defaults.
- Recommendation: Verify this reference manually or remove.

#### Reference #23 — PARTIALLY_VERIFIED
- Cited: Chen, L., et al. (2022). "Cost-effectiveness of telehealth interventions." Health Economics, 31(4), 789-801.
- Issue: Paper exists but year is 2021, not 2022. Volume is 30, not 31.
- Recommendation: Correct to: Chen, L., et al. (2021). Health Economics, 30(4), 789-801.
```

---

## Integration with Workflows

| Workflow | When Citation Check Runs |
|---|---|
| 01-Manuscript Preparation | During literature review (continuous) |
| 02-Pre-Submission | Full reference list validation (mandatory, STOP gate) |
| 04-Peer Review | Reviewer/editor integrity screening |
| 05-Revision | Re-verify any newly added references |
| 06-Production | Final metadata validation |

---

## Quality Thresholds

From `config/quality-thresholds.yaml`:

- **Minimum verification rate**: 95% of references must be VERIFIED
- **Zero tolerance for NOT_FOUND**: Any NOT_FOUND reference must be resolved before submission
- **SUSPICIOUS references**: Must be escalated to human review (STOP gate)
- **PARTIALLY_VERIFIED**: Must be corrected before submission
