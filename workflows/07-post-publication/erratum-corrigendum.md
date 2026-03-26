# Erratum / Corrigendum Workflow

## Purpose

Handle post-publication corrections responsibly and transparently. Errors happen — the integrity of the correction process matters more than the error itself.

---

## Error Classification

| Type | Definition | Examples | Action |
|---|---|---|---|
| **Erratum** | Publisher error introduced during production | Typesetting error, dropped text, figure swap | Publisher issues erratum |
| **Corrigendum** | Author error in the original submission | Incorrect statistic, wrong reference, calculation error | Authors issue corrigendum |
| **Retraction** | Fundamental flaw invalidating the work | Fabricated data, major methodological error, plagiarism | Retraction notice (separate process) |
| **Expression of concern** | Concerns raised but not yet resolved | Under investigation for integrity | Editor issues expression of concern |

---

## Corrigendum Procedure

### Step 1: Error Identification

Document the error:
```yaml
error_report:
  article_doi: "10.xxxx/xxxxx"
  article_title: "Title"
  error_location: "Table 2, Row 3, Column 4"
  error_description: "Reported value is 0.23, should be 0.32"
  error_type: "calculation_error"
  impact_on_conclusions: "Minor — main conclusions unchanged"
  discovered_by: "Author / Reader / Editor"
  discovery_date: "2026-04-15"
```

### Step 2: Impact Assessment

Evaluate whether the error affects:
- [ ] **Conclusions**: Do the main findings change?
- [ ] **Other values**: Are other calculations dependent on this value?
- [ ] **Clinical implications**: Could incorrect information affect patient care?
- [ ] **Policy implications**: Could incorrect information affect policy decisions?
- [ ] **Reproducibility**: Does the error affect others' ability to reproduce the work?

### Step 3: Draft Correction Notice

```markdown
## Corrigendum

**Original article**: [FULL CITATION]
**DOI**: [DOI]

The authors wish to correct an error in the original publication.

**Error**: In Table 2, the cost-effectiveness ratio for the telehealth intervention
was reported as $23,500/QALY. The correct value is $32,500/QALY.

**Cause**: A data entry error during the preparation of the results table.

**Impact**: This correction does not change the main conclusions of the study.
The intervention remains cost-effective at the commonly used willingness-to-pay
threshold of $50,000/QALY.

**Corrected content**: The corrected Table 2 is provided below.

[CORRECTED TABLE]

The authors apologize for this error.
```

### Step 4: Author Approval (STOP-10)

- All authors must review and approve the correction notice
- All authors must agree on the impact assessment
- If there is disagreement about impact, escalate to the editor
- **STOP-10 must be cleared before submission**

### Step 5: Submit to Journal

- Contact the journal editor with the correction notice
- Follow the journal's correction submission process
- Provide both the original and corrected content
- Explain the impact on conclusions

### Step 6: Update Records

After the corrigendum is published:
- [ ] Correction is linked to the original article
- [ ] Original article has a correction notice
- [ ] CrossRef metadata updated
- [ ] Author profiles updated
- [ ] Institutional repository version updated

---

## When Retraction Is Needed

If the error is fundamental and invalidates the work:
1. Contact the editor immediately
2. Follow COPE retraction guidelines
3. The retraction process is editor-led, not author-led
4. Cooperate fully with the investigation
5. A retraction notice must explain the reason clearly

---

## COPE Guidelines for Corrections

Per COPE (Committee on Publication Ethics):
- Corrections should be published promptly
- The correction should be linked to the original article
- The nature of the error should be clearly explained
- The impact on the conclusions should be assessed
- Corrections should be freely accessible
- The original article should have a clear notice directing readers to the correction
