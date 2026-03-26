# Skill: Readability Analysis

## Description

Analyzes text readability using established metrics — Flesch-Kincaid Grade Level, SMOG Index, Gunning Fog Index, Coleman-Liau Index, and Automated Readability Index. Provides audience-appropriate recommendations and identifies specific passages that need simplification.

## When to Use

- During manuscript preparation (Workflow 01) — check draft readability
- During copyediting (Workflow 06) — optimize readability
- During dissemination (Workflow 07) — ensure plain-language summaries are accessible
- When WARN-01 is triggered (readability below threshold)

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `text` | String | Yes | Text content to analyze (full manuscript or section) |
| `target_audience` | Enum | Optional | `general_public`, `clinicians`, `researchers`, `policymakers` |
| `target_journal` | String | Optional | Journal name (for journal-specific targets) |
| `section` | Enum | Optional | `abstract`, `introduction`, `methods`, `results`, `discussion`, `all` |

## Outputs

| Output | Type | Description |
|---|---|---|
| `scores` | Object | All readability metric scores |
| `assessment` | String | Audience-appropriateness assessment |
| `flagged_passages` | List | Specific sentences/paragraphs that are too complex |
| `recommendations` | List | Specific improvement suggestions |

## Step-by-Step Procedure

### Step 1: Calculate Readability Metrics

Using the `textstat` MCP server (preferred) or equivalent:

```python
import textstat

text = "..."  # input text

scores = {
    "flesch_kincaid_grade": textstat.flesch_kincaid_grade(text),
    "smog_index": textstat.smog_index(text),
    "gunning_fog": textstat.gunning_fog(text),
    "coleman_liau_index": textstat.coleman_liau_index(text),
    "automated_readability_index": textstat.automated_readability_index(text),
    "flesch_reading_ease": textstat.flesch_reading_ease(text),
    "dale_chall_readability_score": textstat.dale_chall_readability_score(text),
    "linsear_write_formula": textstat.linsear_write_formula(text),
    "text_standard": textstat.text_standard(text),
}

# Additional statistics
stats = {
    "word_count": textstat.lexicon_count(text),
    "sentence_count": textstat.sentence_count(text),
    "avg_sentence_length": textstat.lexicon_count(text) / textstat.sentence_count(text),
    "syllable_count": textstat.syllable_count(text),
    "avg_syllables_per_word": textstat.syllable_count(text) / textstat.lexicon_count(text),
    "polysyllable_count": textstat.polysyllabcount(text),
    "difficult_words": textstat.difficult_words(text),
}
```

### Step 2: Compare Against Targets

| Audience | FK Grade Target | Flesch RE Target |
|---|---|---|
| General public | 8-10 | 60-70 |
| Policymakers | 10-12 | 50-60 |
| Clinicians | 12-14 | 40-50 |
| Researchers | 12-16 | 30-50 |
| Medical journal (general) | 12-14 | 35-50 |
| Medical journal (specialist) | 14-16 | 25-40 |

### Step 3: Identify Problem Passages

Flag individual sentences or paragraphs that significantly exceed the target:
- Sentences > 40 words
- Sentences with > 3 clauses
- Paragraphs with average FK > target + 4
- Passages with heavy nominalization
- Passages with excessive passive voice

### Step 4: Generate Recommendations

For each flagged passage, provide specific improvement suggestions:
- Break long sentences
- Replace complex words with simpler alternatives
- Convert passive to active voice
- Remove redundancy
- Define technical terms

### Step 5: Section-Level Analysis

If analyzing a full manuscript, provide section-by-section scores:
- Abstract (should be most accessible)
- Introduction (moderate complexity)
- Methods (technical language acceptable)
- Results (clear data presentation)
- Discussion (moderate complexity)

## Quality Criteria

| Criterion | Standard |
|---|---|
| Metric accuracy | Scores match validated textstat library |
| Recommendation specificity | Each recommendation targets a specific passage |
| Audience calibration | Targets match established guidelines for the audience |
| Actionability | Recommendations are concrete (not just "simplify") |

## Cross-References

- Workflows: `workflows/06-production/copyediting.md`, `workflows/07-post-publication/dissemination.md`
- Agents: Production Agent, Author Agent
- Config: `config/quality-thresholds.yaml` (readability thresholds)
- MCP: `textstat` MCP server
