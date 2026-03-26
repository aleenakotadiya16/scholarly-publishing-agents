# Metadata Preparation

## Purpose

Prepare all required metadata for manuscript submission: ORCID identifiers, CRediT author contributions, JATS-XML structured metadata, funding statements, and other required declarations.

---

## Metadata Components

### 1. Author Information

For each author, collect and verify:

| Field | Required | Source |
|---|---|---|
| Full name | Yes | Author |
| ORCID iD | Strongly recommended | https://orcid.org |
| Institutional affiliation(s) | Yes | Author |
| Department | Yes | Author |
| Email (corresponding author) | Yes | Author |
| Country | Yes | Author |
| Equal contribution flag | If applicable | Author agreement |

**ORCID Verification**:
1. Ask each author for their ORCID iD
2. Verify via ORCID API: `https://pub.orcid.org/v3.0/{ORCID}`
3. Confirm the name matches the ORCID profile
4. If author doesn't have ORCID, recommend registration at https://orcid.org/register

### 2. CRediT Author Contributions

Assign CRediT (Contributor Roles Taxonomy) roles to each author using the 14 standardized roles. See `skills/credit-taxonomy.md` for full procedure.

The 14 CRediT roles:
1. Conceptualization
2. Data curation
3. Formal analysis
4. Funding acquisition
5. Investigation
6. Methodology
7. Project administration
8. Resources
9. Software
10. Supervision
11. Validation
12. Visualization
13. Writing – original draft
14. Writing – review & editing

**Output format** (example):
> **Author contributions**: JD: Conceptualization, Methodology, Writing – original draft. AB: Formal analysis, Software, Visualization. CD: Investigation, Data curation. EF: Supervision, Funding acquisition, Writing – review & editing. All authors reviewed and approved the final manuscript.

### 3. Funding Statement

```
This work was supported by [FUNDER NAME] [grant number XXX].
```

If no funding: "This research did not receive any specific grant from funding agencies in the public, commercial, or not-for-profit sectors."

Include:
- Funder name (use FundRef registry names where possible)
- Grant/award numbers
- Role of funder (if any involvement in study design, data collection, analysis, writing, or publication decision)
- If the funder had no role, state this explicitly

### 4. Conflict of Interest Declaration

For each author:
- Financial relationships (consulting, employment, stock ownership, patents)
- Non-financial relationships (personal, institutional, academic)
- If none: "The authors declare no conflicts of interest."

### 5. Data Availability Statement

Options (select appropriate):
- "The data that support the findings of this study are available from the corresponding author upon reasonable request."
- "The data that support the findings of this study are openly available in [REPOSITORY] at [URL/DOI]."
- "The data that support the findings of this study are available from [THIRD PARTY]. Restrictions apply to the availability of these data, which were used under license for this study."
- "Data sharing is not applicable to this article as no new data were created or analyzed in this study."

### 6. Ethics Statements

```yaml
ethics:
  human_subjects:
    approval: "This study was approved by the [COMMITTEE NAME] (reference number: [REF])"
    consent: "Written informed consent was obtained from all participants"
    # or for retrospective studies:
    consent_waiver: "Informed consent was waived due to the retrospective nature of the study"

  animal_subjects:
    approval: "Animal experiments were approved by [COMMITTEE] in accordance with [GUIDELINES]"

  not_applicable: "This study did not involve human or animal subjects"
```

### 7. JATS-XML Metadata

If the journal accepts or requires JATS-XML metadata, prepare structured metadata. See `skills/jats-xml-conversion.md` for the full conversion procedure.

Key JATS-XML elements:
```xml
<article-meta>
  <article-id pub-id-type="doi">10.xxxx/xxxxx</article-id>
  <title-group>
    <article-title>Title</article-title>
  </title-group>
  <contrib-group>
    <contrib contrib-type="author">
      <contrib-id contrib-id-type="orcid">0000-0000-0000-0000</contrib-id>
      <name><surname>Last</surname><given-names>First</given-names></name>
      <aff>Affiliation</aff>
      <role vocab="credit">Conceptualization</role>
    </contrib>
  </contrib-group>
  <pub-date>...</pub-date>
  <kwd-group>
    <kwd>keyword1</kwd>
  </kwd-group>
  <funding-group>
    <award-group>
      <funding-source>Funder Name</funding-source>
      <award-id>Grant Number</award-id>
    </award-group>
  </funding-group>
</article-meta>
```

---

## Metadata Completeness Check

Before proceeding to Workflow 03 (Submission), verify:

- [ ] All author names spelled correctly and consistently
- [ ] All ORCID iDs verified
- [ ] All affiliations current and complete
- [ ] CRediT roles assigned to all authors, all roles assigned to at least one author
- [ ] Funding statement complete and accurate
- [ ] COI declarations from all authors
- [ ] Data availability statement appropriate for the study
- [ ] Ethics statements complete with approval numbers
- [ ] AI disclosure statement approved (STOP-03 cleared)
- [ ] Keywords finalized (MeSH terms where appropriate)
- [ ] Running title within character limit
- [ ] Corresponding author contact information complete
