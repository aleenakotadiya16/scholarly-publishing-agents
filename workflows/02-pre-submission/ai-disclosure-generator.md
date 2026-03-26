# AI Disclosure Statement Generator

## Purpose

Generate a publisher-compliant AI disclosure statement that accurately describes how AI tools were used during manuscript preparation.

---

## Procedure

### Step 1: Identify AI Usage

Gather information about all AI tool usage during manuscript preparation:

```yaml
ai_usage:
  tools:
    - name: "Claude"
      provider: "Anthropic"
      version: "Claude 3.5 Sonnet, January 2026"
      purposes:
        - "Language editing and clarity improvement"
        - "Literature search assistance"
        - "Formatting compliance checking"
      sections_involved:
        - "Introduction (language editing)"
        - "Methods (standardized statistical language)"
        - "Discussion (structural organization)"
      sections_not_involved:
        - "Results (entirely author-generated)"
        - "All figures and tables"
      human_oversight: "All AI-generated suggestions reviewed, edited, and approved by all authors"
```

### Step 2: Identify Target Publisher

1. Check `config/publisher-policies.yaml` for the publisher's requirements
2. Check `rules/disclosure-compliance.md` for disclosure format and location
3. Note any journal-specific requirements beyond the publisher standard

### Step 3: Select Template

Choose the appropriate template from `templates/`:
- `templates/ai-disclosure-elsevier.md` — Elsevier journals
- `templates/ai-disclosure-springer.md` — Springer Nature journals
- `templates/ai-disclosure-wiley.md` — Wiley journals
- `templates/ai-disclosure-taylor-francis.md` — Taylor & Francis journals
- `templates/ai-disclosure-sage.md` — SAGE journals

### Step 4: Generate Disclosure

Fill in the template with specific details from the AI usage log:

1. Name each AI tool with provider and version
2. Describe specific purposes (not just "writing assistance")
3. Identify which sections were AI-assisted
4. Describe the human oversight process
5. Include the accountability statement

### Step 5: Place Disclosure

Place the disclosure in the correct manuscript location:
- **Elsevier**: Dedicated section before References ("Declaration of Generative AI...")
- **Springer Nature**: Methods or Acknowledgements (check specific journal)
- **Wiley**: Acknowledgements or dedicated section (check specific journal)
- **Taylor & Francis**: Separate declaration (submitted during submission)
- **SAGE**: Acknowledgements or Methods (check specific journal)

### Step 6: Author Approval (STOP-03)

Present the disclosure to the author for review:
- Does it accurately represent all AI use?
- Is any AI use missing from the disclosure?
- Is the wording appropriate for the context?
- **Author must explicitly approve before inclusion**

---

## Common Disclosure Patterns

### Pattern A: Language Editing Only
> "During the preparation of this work, the author(s) used [TOOL NAME with version] for language editing and improving readability. After using this tool, the author(s) reviewed and edited the content as needed and take(s) full responsibility for the content of the publication."

### Pattern B: Literature Search + Writing
> "The author(s) used [TOOL NAME with version] to assist with literature search and identification of relevant studies, and for language editing of the Introduction and Discussion sections. All identified references were independently verified against CrossRef and PubMed databases. All AI-generated text was reviewed, substantially edited, and approved by all authors, who take full responsibility for the content."

### Pattern C: Data Analysis Assistance
> "The author(s) used [TOOL NAME with version] to assist with statistical code generation for data analysis. All code was reviewed and validated by [Author Name]. The analysis was independently verified by running the code on the original dataset. Results were interpreted solely by the authors. The AI tool was also used for language editing. Authors take full responsibility for all content and analyses."

### Pattern D: Comprehensive Use
> "[TOOL NAME with version] was used during the preparation of this manuscript for the following purposes: (1) literature search assistance — all identified references were independently verified; (2) language editing of the Introduction, Methods, and Discussion sections; (3) generation of standardized statistical methods descriptions; (4) formatting compliance checking against journal requirements. The AI tool was not used for data analysis, results interpretation, or generation of figures or tables. All AI-assisted content was reviewed, substantially edited, and approved by all authors. The authors take full responsibility for all content in this publication."

---

## What NOT to Include

- Do not disclose basic spell-checking or grammar tools (unless journal specifically requires it)
- Do not include reference manager software (EndNote, Zotero) — these are not generative AI
- Do not include standard statistical software (SPSS, Stata, R) — unless AI-specific features were used
- Do not overstate AI involvement (this can actually raise red flags)
- Do not understate AI involvement (this is an ethics violation)
