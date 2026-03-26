# Typesetting Quality Assurance

## Purpose

Verify the quality of the typeset manuscript before sending author proofs, checking layout, figure/table integrity, cross-references, and overall visual quality.

---

## QA Checklist

### Layout and Formatting

- [ ] **Page layout**: Margins, columns, headers, footers correct per journal template
- [ ] **Font**: Correct typeface and size throughout (body, headings, captions)
- [ ] **Line spacing**: Correct for the journal's production style
- [ ] **Paragraph spacing**: Consistent throughout
- [ ] **Page breaks**: No orphan headings (heading at bottom of page with text on next page)
- [ ] **Widows/orphans**: No single lines at top/bottom of pages
- [ ] **Hyphenation**: Appropriate word breaks (no breaking technical terms or author names)

### Text Integrity

- [ ] **No missing text**: All content from the accepted manuscript is present
- [ ] **No duplicated text**: No paragraphs or sections accidentally duplicated
- [ ] **Special characters**: Greek letters, mathematical symbols, accented characters render correctly
- [ ] **Superscripts/subscripts**: Correctly rendered (especially in chemical formulas, statistical notation)
- [ ] **Equations**: Correctly typeset with proper formatting
- [ ] **Abbreviations**: All abbreviations defined at first use

### Figures

- [ ] **All figures present**: Every figure referenced in text is included
- [ ] **Figure quality**: Resolution meets journal requirements (typically ≥300 DPI for print)
- [ ] **Figure placement**: Near first text reference (or per journal layout policy)
- [ ] **Figure labels**: Axes labeled, legends present, text readable at print size
- [ ] **Figure numbering**: Sequential and matches text references
- [ ] **Figure captions**: Present, accurate, and correctly placed
- [ ] **Color accuracy**: Colors render correctly (check if print will be grayscale)

### Tables

- [ ] **All tables present**: Every table referenced in text is included
- [ ] **Table formatting**: Consistent with journal style (ruling lines, cell spacing)
- [ ] **Table numbering**: Sequential and matches text references
- [ ] **Table titles**: Present, descriptive, correctly placed (above table)
- [ ] **Table notes**: Footnotes present and correctly referenced
- [ ] **Data accuracy**: Numbers match the accepted manuscript
- [ ] **Alignment**: Decimal alignment in numerical columns

### References

- [ ] **All references present**: Complete reference list
- [ ] **Numbering**: Sequential and matches in-text citations
- [ ] **Formatting**: Consistent with journal style
- [ ] **DOIs/URLs**: Present and formatted correctly (no broken links)
- [ ] **Special characters**: Author names with accented characters render correctly

### Cross-References

- [ ] **In-text figure references**: Point to correct figures
- [ ] **In-text table references**: Point to correct tables
- [ ] **Section cross-references**: Correctly linked
- [ ] **Reference citations**: Numbered correctly and linked
- [ ] **Supplementary material references**: Point to correct supplements

### Metadata

- [ ] **Running header/title**: Correct and within character limits
- [ ] **Author names**: Correctly spelled, in correct order
- [ ] **Affiliations**: Correctly mapped to authors
- [ ] **Corresponding author**: Correctly identified with contact info
- [ ] **Article type**: Correctly labeled
- [ ] **DOI**: Displayed correctly
- [ ] **Received/accepted dates**: Correct

---

## Common Typesetting Errors

| Error | Detection |
|---|---|
| **Dropped figures** | Figure referenced in text but missing from proof |
| **Figure swap** | Figure numbers don't match actual figures |
| **Table data errors** | Numbers changed during typesetting (compare with manuscript) |
| **Special character corruption** | μ becomes m, β becomes b, ≤ becomes <= |
| **Reference reordering** | References renumbered incorrectly after typesetting |
| **Missing superscripts** | Footnote markers or citation numbers not superscripted |
| **Incorrect line breaks** | Equations split incorrectly across lines |
| **Color space issues** | CMYK vs RGB color shifts |

---

## QA Report

```markdown
## Typesetting QA Report

**Manuscript**: [MS-ID]
**Journal**: [JOURNAL]
**Proof version**: 1
**Date**: [DATE]

### Issues Found

#### Critical (must fix before proofs to author)
1. Figure 3 appears to be Figure 4 (figures swapped) — Page 12
2. Table 2, Row 3: value shows "0.32" but manuscript says "0.23" — Page 9

#### Important (flag for author attention in proofs)
3. Author name "Müller" rendering as "Muller" — Page 1
4. Greek letter α in equation on Page 7 not rendering

#### Minor (fix in-house)
5. Widowed heading on Page 14
6. Inconsistent en-dash vs. hyphen in number ranges

### Summary
- Critical issues: 2 (must fix)
- Important issues: 2 (flag for author)
- Minor issues: 2 (fix in-house)
```
