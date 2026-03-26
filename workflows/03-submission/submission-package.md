# Submission Package Assembly

## Purpose

Assemble a complete submission package with all required files and declarations, verify completeness against journal requirements, and present for author approval (STOP-04).

---

## Standard Package Components

### Required Files

| Component | Format | Notes |
|---|---|---|
| Manuscript | .docx or .pdf (journal-dependent) | Clean copy, no tracked changes |
| Cover letter | .pdf or entered in submission system | Signed by corresponding author |
| Title page | Separate file or within manuscript | Per journal preference |
| Figures | .tiff, .eps, .pdf, or .jpg (≥300 DPI) | Each figure as separate file |
| Tables | Within manuscript or separate files | Editable format (not images) |
| Supplementary materials | Various formats | Clearly labeled (Table S1, Figure S1) |

### Required Declarations

| Declaration | Content |
|---|---|
| Author contributions | CRediT roles for all authors |
| Conflicts of interest | All authors' COI statements |
| Funding | Funding sources and grant numbers |
| Ethics approval | Committee name and approval number |
| Informed consent | Statement of consent obtained |
| Data availability | Statement on data access |
| AI disclosure | Per publisher requirements |

### Optional Components (Journal-Dependent)

| Component | When Required |
|---|---|
| Suggested reviewers | Most journals request 3-5 |
| Excluded reviewers | When conflicts exist |
| Reporting checklist | CONSORT, STROBE, PRISMA, etc. |
| ORCID iDs | Increasingly required for all authors |
| Graphical abstract | Some journals require/offer this |
| Highlights | Some journals (e.g., Elsevier) request key findings as bullet points |
| Author agreement form | Confirming all authors approve submission |
| Copyright transfer / license | Some journals require at submission |

---

## Assembly Procedure

### Step 1: Gather All Components

Create a checklist based on the target journal's requirements:

```markdown
## Submission Checklist for [JOURNAL NAME]

### Files
- [ ] Manuscript (main text): [filename.docx]
- [ ] Cover letter: [cover-letter.pdf]
- [ ] Figure 1: [fig1-high-res.tiff]
- [ ] Figure 2: [fig2-high-res.tiff]
- [ ] Table S1 (supplementary): [tableS1.docx]
- [ ] PRISMA checklist: [prisma-checklist.pdf]

### Metadata (entered in submission system)
- [ ] All author names, affiliations, ORCID iDs
- [ ] Corresponding author email
- [ ] Keywords / subject classifications
- [ ] Abstract (copy for submission system)
- [ ] Suggested reviewers (3-5)
- [ ] Excluded reviewers (if any)

### Declarations
- [ ] COI statement
- [ ] Funding statement
- [ ] Ethics approval number
- [ ] Data availability statement
- [ ] AI disclosure statement
- [ ] Author contributions (CRediT)
```

### Step 2: Verify File Quality

For each file:
1. Open and verify content is correct and complete
2. Check formatting meets journal requirements
3. Verify figures are at required resolution
4. Confirm supplementary materials are correctly referenced in main text
5. Check file sizes are within journal limits

### Step 3: Final Consistency Check

Cross-verify:
- [ ] Author names match across manuscript, cover letter, and metadata
- [ ] Title matches across all documents
- [ ] Abstract in manuscript matches abstract in submission system
- [ ] Reference to figures/tables in text matches actual figures/tables
- [ ] Supplementary material references in text match actual supplementary files
- [ ] Running title is within character limit
- [ ] Word count is within limit

### Step 4: STOP-04 — Author Approval

Present the complete package to the author:

```markdown
## Submission Package Summary

**Journal**: [JOURNAL NAME]
**Manuscript**: [TITLE]
**Files**: [N] files ready for upload
**Missing items**: [NONE / list any missing items]

### Package Contents
1. ✅ Manuscript (3,450 words) — within limit
2. ✅ Cover letter — addressed to [EDITOR NAME]
3. ✅ Figure 1 (600 DPI TIFF)
4. ✅ Figure 2 (600 DPI TIFF)
5. ✅ Figure 3 (300 DPI TIFF)
6. ✅ Supplementary Table S1
7. ✅ STROBE checklist
8. ✅ All declarations complete

### ⚠️ Reminders
- You will need to enter author metadata in the submission portal
- Have all co-authors confirmed their approval?
- Do you have the ethics approval letter ready to upload?

**AWAITING YOUR APPROVAL TO PROCEED WITH SUBMISSION**
```

**The author performs the actual submission** — the agent does NOT submit on the author's behalf.

---

## Post-Submission Record Keeping

After the author submits, record:

```yaml
submission_record:
  journal: "Health Economics"
  publisher: "Wiley"
  manuscript_id: "HEC-2026-0123" # assigned by journal
  submission_date: "2026-01-20"
  corresponding_author: "Dylan Mordaunt"
  article_type: "Original Research"
  expected_initial_decision: "2026-03-17" # ~8 weeks
  status: "Under Review"
  notes: "Submitted via ScholarOne"
```
