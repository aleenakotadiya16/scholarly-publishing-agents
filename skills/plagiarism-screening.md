# Skill: Plagiarism Screening

## Description

Screens manuscript text for potential plagiarism, text recycling, and excessive similarity to published works. Identifies direct copying, close paraphrasing, structural plagiarism, and self-plagiarism (text recycling).

## When to Use

- During peer review integrity screening (Workflow 04)
- Author self-check before submission (Workflow 02)
- When similarity concerns are raised during review

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `manuscript_text` | Text | Yes | Full text of the manuscript |
| `known_sources` | List | Optional | Known source documents (e.g., author's previous publications for self-plagiarism check) |
| `threshold` | Float | Optional | Similarity threshold for flagging (default: from `config/quality-thresholds.yaml`) |

## Outputs

| Output | Type | Description |
|---|---|---|
| `overall_similarity` | Float 0-100 | Overall similarity percentage |
| `flagged_passages` | List | Passages with high similarity to known sources |
| `source_matches` | List | Identified source documents for each flagged passage |
| `assessment` | String | Classification: acceptable / elevated / concerning |
| `recommendations` | List | Specific actions for flagged passages |

## Step-by-Step Procedure

### Step 1: Text Preparation
- Strip references section (high similarity expected and acceptable)
- Strip common phrases and standard methodology language
- Identify quoted material (properly attributed quotes are acceptable)
- Segment text into analyzable chunks (typically sentence or paragraph level)

### Step 2: Similarity Detection

Types of similarity to detect:

| Type | Description | Acceptable? |
|---|---|---|
| **Direct copy** | Verbatim text without quotation marks | No |
| **Close paraphrase** | Minor word changes, same structure | Depends on attribution |
| **Mosaic plagiarism** | Phrases from multiple sources stitched together | No |
| **Self-plagiarism** | Recycled from author's own prior work | Depends on journal policy |
| **Structural** | Same argument structure, different words | Borderline |
| **Translation** | Translated from another language without credit | No |
| **Common phrases** | Standard scientific language ("patients were randomized to...") | Yes |
| **Quoted material** | Properly quoted and cited | Yes |
| **Methods language** | Standard methodology descriptions | Usually acceptable |

### Step 3: Source Identification

For flagged passages:
1. Identify the likely source document
2. Provide DOI/URL of the source
3. Show side-by-side comparison (flagged text vs. source)
4. Classify the similarity type

### Step 4: Context Assessment

Not all similarity is plagiarism. Assess context:
- **Methods sections** commonly reuse standard language (especially for validated instruments)
- **Background sections** may legitimately summarize prior work
- **Quotes** with proper attribution are acceptable
- **Self-citation** with appropriate references is normal

### Step 5: Generate Report

```markdown
## Plagiarism Screening Report

### Overall Similarity: 12%

### Assessment: Acceptable
Most similarity is in Methods section (standard methodology language)
and properly cited quotations.

### Flagged Passages

#### Passage 1 — LOW CONCERN
- Location: Methods, paragraph 3
- Similarity: 89% match with Smith et al. (2023)
- Type: Standard methodology description
- Assessment: Acceptable — standard description of a validated instrument
- Action: None needed

#### Passage 2 — MODERATE CONCERN
- Location: Discussion, paragraph 2
- Similarity: 75% match with Author's previous paper (2024)
- Type: Self-plagiarism / text recycling
- Assessment: Check journal policy on text recycling
- Action: Rewrite or cite previous publication explicitly

#### Passage 3 — HIGH CONCERN
- Location: Introduction, paragraph 4
- Similarity: 92% match with Jones et al. (2022)
- Type: Close paraphrase without citation
- Assessment: Needs citation or rewrite
- Action: Add citation to Jones et al. or rewrite substantially
```

## Quality Criteria

| Criterion | Standard |
|---|---|
| False positive rate | < 10% (standard methods language correctly classified) |
| Detection sensitivity | Catches direct copying with > 95% accuracy |
| Context awareness | Distinguishes acceptable from problematic similarity |
| Source accuracy | Correct source identified for > 90% of flagged passages |

## Cross-References

- Rules: `rules/quality-gates.md` (WARN-10 for elevated similarity)
- Workflows: `workflows/04-peer-review/integrity-screening.md`
- Agents: Integrity Agent
- Config: `config/quality-thresholds.yaml` (similarity thresholds)
- Tools: iThenticate, Turnitin (publisher-authorized tools)
