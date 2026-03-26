# AI-Assisted Copyediting with Readability Analysis

## Purpose

Polish the accepted manuscript for publication through comprehensive copyediting, readability optimization, and consistency checking — without altering the technical meaning.

---

## Copyediting Scope

### What Copyediting Covers

| Category | Examples |
|---|---|
| **Grammar** | Subject-verb agreement, tense consistency, article usage |
| **Spelling** | Typos, consistent spelling (British/American), technical terms |
| **Punctuation** | Comma usage, hyphenation, semicolons, en/em dashes |
| **Style consistency** | Abbreviation usage, capitalization, number formatting |
| **Clarity** | Ambiguous sentences, unclear antecedents, wordiness |
| **Academic tone** | Appropriate formality, hedging language, objective voice |
| **Accessibility** | Plain language where possible, defined abbreviations |

### What Copyediting Does NOT Cover

- **Technical content**: Never change the meaning of methods, results, or conclusions
- **Data**: Never modify numbers, statistics, or values
- **Citations**: Never add, remove, or modify references (flag issues instead)
- **Scientific claims**: Never alter the strength or direction of findings
- **Author voice**: Minimize changes to the author's distinctive style

---

## Readability Analysis

### Readability Metrics

Use `skills/readability-analysis.md` (and the `textstat` MCP server if available):

| Metric | Formula/Basis | Target for Medical Journals | Target for Public Health |
|---|---|---|---|
| **Flesch-Kincaid Grade Level** | Sentence length + syllables per word | 12-16 | 8-12 |
| **SMOG Index** | Polysyllabic word count | 12-16 | 10-14 |
| **Gunning Fog Index** | Sentence length + complex words | 12-16 | 10-14 |
| **Coleman-Liau Index** | Characters per word + sentences per 100 words | 12-16 | 10-14 |
| **Automated Readability Index** | Characters per word + words per sentence | 12-16 | 10-14 |
| **Flesch Reading Ease** | Inverse of FK Grade Level | 30-50 (difficult) | 50-70 (standard) |

### Section-Specific Targets

| Section | Audience | Readability Target |
|---|---|---|
| Abstract | Broad academic | Moderate (FK 12-14) |
| Introduction | Field researchers | Moderate-difficult (FK 12-16) |
| Methods | Specialists | Technical language acceptable (FK 14-18) |
| Results | Specialists | Clear data presentation (FK 12-16) |
| Discussion | Broad academic | Moderate (FK 12-14) |
| Plain-language summary | General public | Easy (FK 8-10) |

### Readability Improvement Strategies

| Issue | Strategy |
|---|---|
| **Long sentences** | Break into shorter sentences; target < 25 words average |
| **Passive voice** | Convert to active voice where meaning is preserved |
| **Nominalizations** | Convert noun forms back to verbs (e.g., "utilization" → "use") |
| **Jargon** | Define technical terms at first use; use simpler alternatives where possible |
| **Nested clauses** | Unpack complex sentences into sequential statements |
| **Double negatives** | Replace with positive statements |
| **Redundancy** | Remove unnecessary words ("in order to" → "to") |

---

## Consistency Checks

### Internal Consistency

- [ ] Abbreviations defined at first use and used consistently thereafter
- [ ] Numbers formatted consistently (spelled out < 10 or always numerals per journal style)
- [ ] Statistical notation consistent (P vs. p, < vs. ≤, × vs. x)
- [ ] Table/figure numbering sequential and correctly referenced
- [ ] Reference style consistent throughout
- [ ] Headings consistent in format (capitalization, numbering)
- [ ] Units consistent (kg not kilograms/kg mix; always SI)
- [ ] Drug names: generic (lowercase) vs. brand (capitalized) — follow journal style
- [ ] Gene/protein nomenclature follows conventions (italic genes, roman proteins)

### Cross-Document Consistency

- [ ] Abstract matches main text (same numbers, same conclusions)
- [ ] Author list matches across title page, manuscript, and metadata
- [ ] Funding information consistent across manuscript and submission system
- [ ] Ethics approval number consistent across manuscript and cover letter

---

## Copyediting Output

For each suggested change:

```markdown
### Change #14
- **Location**: Page 8, Line 167
- **Original**: "The utilization of telehealth services resulted in a significant reduction in costs."
- **Suggested**: "Using telehealth services significantly reduced costs."
- **Reason**: Active voice, reduced nominalization, improved clarity
- **Impact**: Language only — no change to meaning
- **Author approval needed**: No (minor language edit)
```

For substantive changes:

```markdown
### Change #27 — REQUIRES AUTHOR REVIEW
- **Location**: Page 12, Line 245
- **Original**: "This demonstrates that telehealth is cost-effective."
- **Suggested**: "These findings suggest that telehealth may be cost-effective in this setting."
- **Reason**: Original statement is too strong for the evidence; the study only demonstrates cost-effectiveness in the modeled scenario
- **Impact**: Modifies the strength of the claim
- **Author approval needed**: YES — this changes the meaning of the statement
```

---

## CRITICAL RULE

**Never change the meaning of technical content.** If there is any doubt about whether a copyedit changes meaning, flag it for author review rather than making the change.
