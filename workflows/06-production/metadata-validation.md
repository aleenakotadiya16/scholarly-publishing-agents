# Metadata Validation

## Purpose

Validate all metadata for accurate indexing, discoverability, and interoperability. Ensure DOI registration, CrossRef deposit, JATS-XML compliance, and correct author/affiliation data.

---

## Metadata Components to Validate

### 1. DOI (Digital Object Identifier)

| Check | Method |
|---|---|
| **DOI assigned** | Verify DOI has been assigned by the publisher |
| **DOI format** | Must follow `10.{registrant}/{suffix}` format |
| **DOI resolution** | DOI resolves to the correct article landing page |
| **DOI in manuscript** | DOI displayed correctly in the published version |

### 2. CrossRef Metadata Deposit

Verify that the CrossRef metadata record contains:

```xml
<doi_record>
  <journal>
    <journal_metadata>
      <full_title>Journal Name</full_title>
      <issn>XXXX-XXXX</issn>
    </journal_metadata>
    <journal_article>
      <titles>
        <title>Article Title</title>
      </titles>
      <contributors>
        <person_name contributor_role="author" sequence="first">
          <given_name>First</given_name>
          <surname>Last</surname>
          <ORCID>https://orcid.org/0000-0000-0000-0000</ORCID>
        </person_name>
      </contributors>
      <publication_date>
        <year>2026</year>
      </publication_date>
      <doi_data>
        <doi>10.xxxx/xxxxx</doi>
        <resource>https://...</resource>
      </doi_data>
    </journal_article>
  </journal>
</doi_record>
```

Validate:
- [ ] Title matches published article exactly
- [ ] All authors listed with correct names
- [ ] ORCID iDs included for all authors who provided them
- [ ] Publication date correct
- [ ] DOI correct
- [ ] Resource URL correct and functional
- [ ] Funding information deposited (Fundref)
- [ ] License information deposited (Creative Commons type)
- [ ] References deposited (for citation linking)

### 3. JATS-XML Validation

If the journal produces JATS-XML (see `skills/jats-xml-conversion.md`):

- [ ] Valid against JATS DTD (use JATS4R validator)
- [ ] Article type correctly tagged
- [ ] All sections properly structured
- [ ] Mathematics encoded correctly (MathML or LaTeX)
- [ ] Tables encoded as structured data (not images)
- [ ] Figures referenced with correct file paths
- [ ] All metadata elements present and correct

### 4. Author/Affiliation Verification

- [ ] Author names match the accepted manuscript
- [ ] Author order is correct
- [ ] All affiliations listed and correctly mapped
- [ ] Corresponding author correctly identified
- [ ] ORCID iDs present and valid
- [ ] Equal contribution noted where applicable
- [ ] CRediT roles included (if journal publishes them)

### 5. Abstract and Keywords

- [ ] Abstract present in metadata
- [ ] Abstract matches the manuscript abstract exactly
- [ ] Keywords/MeSH terms present
- [ ] Subject classifications assigned

### 6. Funding and Grants

- [ ] Funder names match Fundref registry
- [ ] Grant/award numbers correct
- [ ] Funder DOIs included where available
- [ ] Open access funding acknowledged if applicable

### 7. License and Access

- [ ] Access level correct (open access / subscription)
- [ ] License type correct (CC-BY, CC-BY-NC, etc.)
- [ ] Embargo period correctly set (if applicable)
- [ ] Self-archiving rights correctly reflected

---

## Validation Tools

| Tool | Purpose | URL |
|---|---|---|
| CrossRef API | Verify DOI metadata | `https://api.crossref.org/works/{DOI}` |
| DOI resolver | Check DOI resolution | `https://doi.org/{DOI}` |
| ORCID API | Verify author identifiers | `https://pub.orcid.org/v3.0/{ORCID}` |
| JATS4R Validator | Validate JATS-XML | `https://validator.jats4r.org/` |
| Fundref API | Verify funder identifiers | `https://api.crossref.org/funders` |

---

## Metadata Validation Report

```markdown
## Metadata Validation Report

**Article**: [TITLE]
**DOI**: 10.xxxx/xxxxx
**Date**: [DATE]

### DOI ✅
- Assigned: 10.xxxx/xxxxx
- Resolves correctly: Yes
- Displayed in manuscript: Yes

### CrossRef Deposit ✅
- Title: Matches ✅
- Authors: 4/4 correct ✅
- ORCID: 3/4 deposited (Author 3 has no ORCID) ⚠️
- Publication date: Correct ✅
- References: 45/45 deposited ✅
- Funding: Deposited with Fundref ID ✅

### JATS-XML ✅
- Valid against JATS 1.3 DTD ✅
- All sections tagged ✅
- Tables structured ✅

### Issues
- Author 3 missing ORCID — contact author to provide
```
