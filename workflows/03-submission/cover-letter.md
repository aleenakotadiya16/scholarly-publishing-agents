# Cover Letter Generation

## Purpose

Draft a compelling, journal-specific cover letter that highlights the manuscript's significance, relevance to the journal's scope, and key findings. A good cover letter can influence the editor's triage decision.

---

## Cover Letter Structure

### 1. Header
- Date
- Editor's name and title (if known — check journal website)
- Journal name
- Publisher address (optional for email submissions)

### 2. Opening Paragraph
- Manuscript title
- Article type (original research, review, etc.)
- Statement that this is a new submission (or resubmission if applicable)
- Confirmation that the work has not been published elsewhere and is not under consideration at another journal

### 3. Significance Paragraph
- What is the research question?
- Why does it matter? (clinical significance, policy implications, knowledge gap)
- What are the key findings?
- How does this advance the field?

### 4. Relevance to Journal
- Why is this journal the right venue for this work?
- Reference recent relevant publications in the journal (verified citations only)
- How does this manuscript fit the journal's scope and readership?

### 5. Technical Summary
- Brief overview of methodology
- Key results (1-2 sentences)
- Main conclusions

### 6. Declarations
- Confirmation of ethical approvals (if applicable)
- Confirmation of author consent and contributions
- Disclosure of conflicts of interest
- AI disclosure (if required in cover letter by journal — e.g., The Lancet)
- Data availability statement (if required in cover letter)

### 7. Suggested Reviewers (if required)
- 3-5 suggested reviewers with rationale
- Include: name, institution, email, brief rationale for selection
- Avoid: close collaborators, co-authors, advisors, people at your institution

### 8. Excluded Reviewers (if applicable)
- Reviewers the author requests be excluded
- Brief, professional reason (e.g., "direct competitor" or "potential conflict of interest")

### 9. Closing
- Thank the editor for considering the manuscript
- Corresponding author's contact information
- All authors' signatures (electronic)

---

## Template

See `templates/cover-letter-template.md` for a ready-to-use template.

---

## Cover Letter Dos and Don'ts

### Do:
- Be specific about why THIS journal (not a generic letter)
- Highlight the novel contribution clearly
- Keep it concise (typically 1 page)
- Mention if any authors are on the journal's editorial board (transparency)
- Include all required declarations per journal guidelines
- Mention if the work was presented at a conference (with details)
- Reference specific recent articles in the journal that relate to your work

### Don't:
- Use generic language ("We are pleased to submit...")
- Oversell the findings (editors are experienced readers)
- Include figures, tables, or supplementary data
- Exceed 1 page unless the journal requires detailed declarations
- Use AI-generated citations in the cover letter without verification
- Copy-paste the abstract as the cover letter body
- Forget to update the journal name if resubmitting to a different journal

---

## Journal-Specific Requirements

Check `config/journal-requirements.yaml` for each journal's cover letter requirements. Common variations:

| Journal | Special Requirements |
|---|---|
| BMJ | Requires structured cover letter with specific headings |
| JAMA | Requires word count, author contributions in cover letter |
| The Lancet | Requires AI disclosure in cover letter |
| PLOS ONE | Requires data availability statement in cover letter |
| Nature | Brief cover letter; significance statement critical |

---

## Quality Check

Before finalizing the cover letter:

- [ ] Editor's name correct and current (check journal website)
- [ ] Journal name spelled correctly (no embarrassing mixups from previous submissions)
- [ ] Manuscript title matches the actual manuscript
- [ ] Key findings accurately represent the results
- [ ] All required declarations present per journal guidelines
- [ ] Suggested reviewers are appropriate (no conflicts)
- [ ] No grammatical errors or typos
- [ ] Tone is professional but not obsequious
- [ ] Length is appropriate (typically < 1 page body text)
- [ ] All citations in the letter are verified
