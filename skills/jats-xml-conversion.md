# Skill: JATS-XML Conversion

## Description

Converts manuscript content and metadata into JATS-XML (Journal Article Tag Suite) format, the standard for structuring journal articles. Supports JATS 1.3 in Blue (publishing), Green (archiving), and Orange (authoring) tag sets.

## When to Use

- During metadata preparation (Workflow 02)
- During production (Workflow 06)
- When journals require XML submission
- For archiving and repository deposit

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `manuscript` | Structured text | Yes | Manuscript content with sections identified |
| `metadata` | Object | Yes | Authors, affiliations, funding, keywords, etc. |
| `references` | List | Yes | Structured reference list |
| `tag_set` | Enum | Optional | `blue` (publishing), `green` (archiving), `orange` (authoring). Default: `green` |

## Outputs

| Output | Type | Description |
|---|---|---|
| `jats_xml` | XML string | Valid JATS-XML document |
| `validation_report` | Object | Validation results against JATS DTD |
| `warnings` | List | Non-critical issues found during conversion |

## Step-by-Step Procedure

### Step 1: Prepare Document Structure

Map manuscript sections to JATS elements:

| Manuscript Section | JATS Element |
|---|---|
| Title | `<article-title>` |
| Abstract | `<abstract>` |
| Keywords | `<kwd-group>` |
| Introduction | `<sec sec-type="intro">` |
| Methods | `<sec sec-type="methods">` |
| Results | `<sec sec-type="results">` |
| Discussion | `<sec sec-type="discussion">` |
| References | `<ref-list>` |
| Acknowledgements | `<ack>` |
| Funding | `<funding-group>` |
| COI | `<fn fn-type="conflict">` |

### Step 2: Build Article Metadata

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE article PUBLIC "-//NLM//DTD JATS (Z39.96) Journal Archiving and Interchange DTD v1.3 20210610//EN"
  "JATS-archivearticle1-3.dtd">
<article article-type="research-article" xml:lang="en">
  <front>
    <journal-meta>
      <journal-id journal-id-type="nlm-ta">J Name Abbrev</journal-id>
      <journal-title-group>
        <journal-title>Full Journal Name</journal-title>
      </journal-title-group>
      <issn pub-type="ppub">XXXX-XXXX</issn>
      <issn pub-type="epub">XXXX-XXXX</issn>
      <publisher>
        <publisher-name>Publisher Name</publisher-name>
      </publisher>
    </journal-meta>
    <article-meta>
      <article-id pub-id-type="doi">10.xxxx/xxxxx</article-id>
      <title-group>
        <article-title>Article Title</article-title>
      </title-group>
      <!-- Contributors, abstract, keywords, funding, etc. -->
    </article-meta>
  </front>
  <body>
    <!-- Sections -->
  </body>
  <back>
    <!-- References, appendices -->
  </back>
</article>
```

### Step 3: Encode Contributors with CRediT Roles

```xml
<contrib-group>
  <contrib contrib-type="author" corresp="yes">
    <contrib-id contrib-id-type="orcid" authenticated="true">
      https://orcid.org/0000-0000-0000-0000
    </contrib-id>
    <name>
      <surname>Mordaunt</surname>
      <given-names>Dylan A.</given-names>
    </name>
    <xref ref-type="aff" rid="aff1"/>
    <role vocab="credit"
          vocab-identifier="https://credit.niso.org/"
          vocab-term="Conceptualization"
          vocab-term-identifier="https://credit.niso.org/contributor-roles/conceptualization/">
      Conceptualization
    </role>
  </contrib>
</contrib-group>
```

### Step 4: Encode References

```xml
<ref-list>
  <ref id="ref1">
    <element-citation publication-type="journal">
      <person-group person-group-type="author">
        <name><surname>Smith</surname><given-names>J.A.</given-names></name>
      </person-group>
      <article-title>Title of the article</article-title>
      <source>Journal Name</source>
      <year iso-8601-date="2024">2024</year>
      <volume>33</volume>
      <issue>5</issue>
      <fpage>1120</fpage>
      <lpage>1135</lpage>
      <pub-id pub-id-type="doi">10.1002/hec.4567</pub-id>
    </element-citation>
  </ref>
</ref-list>
```

### Step 5: Validate

1. Validate against JATS DTD (use xmllint or JATS4R validator)
2. Check all required elements are present
3. Verify all cross-references resolve
4. Confirm character encoding (UTF-8)

## Quality Criteria

| Criterion | Standard |
|---|---|
| DTD validity | Must pass JATS 1.3 DTD validation |
| Completeness | All manuscript sections represented |
| Metadata accuracy | All author, affiliation, funding data correct |
| Reference encoding | All references properly structured |
| Character encoding | UTF-8, all special characters preserved |

## Cross-References

- Workflows: `workflows/02-pre-submission/metadata-preparation.md`, `workflows/06-production/metadata-validation.md`
- Agents: Production Agent
- Standards: JATS 1.3 (NISO Z39.96-2019), JATS4R recommendations
