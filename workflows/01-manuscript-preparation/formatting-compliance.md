# Formatting Compliance Check

## Purpose

Verify that a manuscript draft complies with the target journal's formatting requirements before proceeding to pre-submission checks.

---

## Compliance Checklist

### General Formatting

| Element | Check | Source |
|---|---|---|
| **Word count** | Within journal limit (check `config/journal-requirements.yaml`) | Journal guidelines |
| **Abstract** | Correct structure (structured vs. unstructured), within word limit | Journal guidelines |
| **Keywords** | Correct number, from MeSH or journal-specified vocabulary | Journal guidelines |
| **Heading levels** | Match journal style (numbered vs. unnumbered, caps style) | Journal guidelines |
| **Line spacing** | Double-spaced (standard for most journals) | Journal guidelines |
| **Font** | Times New Roman 12pt or as specified | Journal guidelines |
| **Margins** | 1 inch / 2.54 cm or as specified | Journal guidelines |
| **Page numbers** | Present on all pages | Standard |
| **Line numbers** | Continuous line numbering (required by many journals) | Journal guidelines |

### Section Structure

| Manuscript Type | Expected Structure |
|---|---|
| **Original research** | Title, Abstract, Introduction, Methods, Results, Discussion, References |
| **Systematic review** | Title, Abstract, Introduction, Methods (search, screening, extraction, synthesis), Results, Discussion, References + PRISMA diagram |
| **Case study** | Title, Abstract, Introduction, Case Presentation, Discussion, References |
| **Letter/Commentary** | Title, Body, References (usually unstructured) |
| **Review article** | Title, Abstract, Introduction, [Themed sections], Conclusion, References |

### Reference Formatting

| Style | Common Journals | Example |
|---|---|---|
| **Vancouver** | BMJ, JAMA, Lancet, most medical journals | Numbered in-text, numbered reference list |
| **APA 7th** | Psychology, social sciences | (Author, Year) in-text, alphabetical list |
| **Harvard** | Many UK/Australian journals | (Author Year) in-text, alphabetical list |
| **AMA** | JAMA and AMA-published journals | Superscript numbered, numbered list |
| **NLM** | PubMed-indexed journals | Similar to Vancouver |

### Table and Figure Requirements

| Element | Common Requirements |
|---|---|
| **Table titles** | Above the table, numbered sequentially |
| **Figure legends** | Below the figure or in a separate section |
| **Figure resolution** | Minimum 300 DPI for print; 150 DPI for online-only |
| **Figure format** | TIFF, EPS, or high-resolution PDF (check journal) |
| **Table format** | Editable (not images); use journal table template if provided |
| **Color figures** | Check if extra charges apply for print color |
| **Supplementary materials** | Formatted per journal requirements; clearly labeled |

### Ethical and Regulatory

| Element | Check |
|---|---|
| **Ethics approval** | Statement present with ethics committee name and approval number |
| **Informed consent** | Statement present (for human subjects research) |
| **Trial registration** | Registration number included (for clinical trials — ICMJE requirement) |
| **Data availability** | Data availability statement present (many journals now require this) |
| **Funding** | Funding statement present (even if no funding received) |
| **Conflicts of interest** | COI statement present for all authors |
| **AI disclosure** | AI use disclosure present per publisher requirements |

---

## Automated Formatting Checks

The following can be checked programmatically:

```yaml
automated_checks:
  - name: word_count
    action: Count words in main text (excluding abstract, references, tables, figures)
    threshold: from config/journal-requirements.yaml

  - name: abstract_word_count
    action: Count words in abstract
    threshold: from config/journal-requirements.yaml

  - name: abstract_structure
    action: Check for required headings (Background, Methods, Results, Conclusions)
    applies_to: journals requiring structured abstracts

  - name: keyword_count
    action: Count keywords
    threshold: from config/journal-requirements.yaml

  - name: reference_count
    action: Count references
    threshold: from config/journal-requirements.yaml (if limit exists)

  - name: reference_style
    action: Check reference formatting against expected style
    target: from config/journal-requirements.yaml

  - name: heading_hierarchy
    action: Verify heading levels are properly nested
    check: no skipped levels (e.g., H1 → H3 without H2)

  - name: required_sections
    action: Check for presence of all required sections
    sections: from config/journal-requirements.yaml

  - name: line_numbering
    action: Verify continuous line numbers present
    applies_to: journals requiring line numbers

  - name: ethical_statements
    action: Check for ethics, consent, COI, funding, data availability statements
    check: presence and location
```

---

## Common Formatting Issues

1. **Abstract exceeds word limit** — Most common issue; recommend specific cuts
2. **Reference style mismatch** — Author used APA but journal requires Vancouver
3. **Missing structured abstract headings** — Many medical journals require structured abstracts
4. **Figures not meeting resolution requirements** — Especially common with screen captures
5. **Table formatting** — Tables submitted as images instead of editable formats
6. **Missing ethical statements** — Ethics approval, consent, COI often forgotten
7. **Supplementary material format** — Not following journal's supplementary file guidelines
8. **Title page format** — Missing required elements (running title, word count, author contact details)

---

## Output

Generate a formatting compliance report:

```markdown
## Formatting Compliance Report

Target Journal: BMJ
Publisher: BMJ Publishing Group

### ✅ Compliant
- Word count: 3,450 (limit: 4,000)
- Reference style: Vancouver (correct)
- Heading structure: IMRAD (correct)
- Ethics approval: Present

### ⚠️ Warnings (WARN-03)
- Abstract: 287 words (limit: 250) — needs reduction
- Keywords: 4 provided (requirement: 3-6) — acceptable but check MeSH terms
- Line numbering: Not present — required by BMJ

### ❌ Must Fix
- Missing: Data availability statement (required by BMJ since 2023)
- Missing: AI disclosure statement (if AI tools were used)
- Figure 2: Resolution appears below 300 DPI
```
