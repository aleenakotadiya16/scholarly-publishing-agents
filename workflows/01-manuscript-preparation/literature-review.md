# Literature Search and Citation Verification

## Purpose

Conduct a thorough, systematic literature search to support manuscript preparation, with mandatory verification of every identified reference.

---

## Search Strategy

### Step 1: Define Search Parameters

Work with the author to establish:
- **Research question**: Structured using PICO(S) for clinical questions or equivalent framework
- **Key concepts and terms**: Include synonyms, MeSH terms, and variant spellings
- **Databases to search**: PubMed, Embase, Cochrane Library, Web of Science, Scopus (field-dependent)
- **Date range**: Typically last 5-10 years, unless historical context needed
- **Language restrictions**: English-only or multilingual
- **Inclusion/exclusion criteria**: Study types, population, outcomes

### Step 2: Conduct Searches

For each database:
1. Construct search string using Boolean operators (AND, OR, NOT)
2. Apply MeSH terms and free-text combinations
3. Record the exact search strategy (for reproducibility)
4. Document: database, date searched, search string, number of results

**Example PubMed search for a health economics paper**:
```
("health economics"[MeSH] OR "cost-effectiveness"[tiab] OR "cost-benefit analysis"[tiab])
AND ("telehealth"[MeSH] OR "telemedicine"[tiab] OR "remote consultation"[tiab])
AND ("systematic review"[pt] OR "meta-analysis"[pt] OR "randomized controlled trial"[pt])
AND 2020:2026[dp]
```

### Step 3: Screen Results

1. Title and abstract screening against inclusion/exclusion criteria
2. Full-text screening for borderline cases
3. Record reasons for exclusion
4. For systematic reviews: generate PRISMA flow diagram data

### Step 4: Citation Verification (MANDATORY)

**Every reference added to the manuscript must be verified.** Invoke `skills/citation-verification.md`:

1. Extract structured reference data (authors, title, journal, year, DOI)
2. Verify each reference against CrossRef and/or PubMed
3. Confirm all metadata fields match
4. Flag any unverifiable references
5. Generate verification report

### Step 5: Organize References

- Structure references by theme, methodology, or chronology (as appropriate)
- Identify key papers vs. supporting evidence
- Note any gaps in the literature
- Export to reference manager (EndNote, Zotero, Mendeley) if available

---

## For Systematic Reviews and Scoping Reviews

If the manuscript is a systematic review or scoping review, additional requirements apply:

1. **Pre-register the protocol** on PROSPERO or OSF
2. **Follow PRISMA 2020 guidelines** (invoke `skills/prisma-compliance.md`)
3. **Document the complete search strategy** in the Methods section
4. **Use at least 2 databases** (recommended: 3+)
5. **Have at least 2 independent screeners** (human)
6. **Record all screening decisions** with reasons
7. **Generate a PRISMA flow diagram**

AI can assist with:
- Constructing and refining search strategies
- Title/abstract screening (as a second screener, not primary)
- Data extraction template creation
- PRISMA checklist completion

AI must NOT:
- Make final inclusion/exclusion decisions (human decision)
- Fabricate search results or screening outcomes
- Generate data extraction results from non-existent papers

---

## Citation Tracking

For key papers in the field:
1. **Forward citation search**: Who has cited this paper since publication? (Google Scholar, Semantic Scholar)
2. **Backward citation search**: What did this paper cite? Follow reference chains.
3. **Related articles**: Use PubMed "similar articles" and database recommendation engines.

---

## Reference Quality Assessment

Rate each reference for quality:

| Criterion | Assessment |
|---|---|
| **Relevance** | Directly relevant / Tangentially relevant / Context only |
| **Evidence level** | Systematic review / RCT / Cohort / Case-control / Case series / Expert opinion |
| **Recency** | Current (< 3 years) / Recent (3-5 years) / Older (5-10 years) / Historical (> 10 years) |
| **Verification status** | Verified / Partially verified / Unverified |
| **Journal quality** | Indexed (PubMed/Scopus/WoS) / DOAJ-listed / Not indexed |

---

## Tools and APIs

| Tool | Purpose | API |
|---|---|---|
| PubMed/NCBI | Biomedical literature search | E-utilities API |
| CrossRef | DOI-based reference verification | CrossRef REST API |
| OpenAlex | Open scholarly metadata | OpenAlex API |
| Semantic Scholar | AI-powered literature discovery | Semantic Scholar API |
| Google Scholar | Broad literature search | No official API (use with caution) |
| ASReview | AI-assisted systematic review screening | Python library |
| OSF | Protocol registration | OSF API |

---

## Output

The literature review process should produce:
1. **Search strategy documentation** (for Methods section)
2. **Verified reference list** (with citation verification report)
3. **Literature summary** (organized by theme or methodology)
4. **Gap analysis** (what's missing from the literature)
5. **PRISMA flow diagram** (if systematic review)
