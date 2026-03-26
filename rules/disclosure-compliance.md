# AI Disclosure Compliance Rules

## Overview

Every major academic publisher now requires disclosure of AI use in manuscript preparation. Requirements vary significantly by publisher, and some journals within a publisher have additional requirements. **Always check the specific journal's author guidelines in addition to the publisher-level policy.**

This document provides structured disclosure requirements as of early 2026. Policies evolve — always verify current requirements at the publisher's website before submission.

---

## Publisher Disclosure Requirements

### Elsevier

| Requirement | Details |
|---|---|
| **Disclosure location** | Dedicated "Declaration of Generative AI and AI-assisted technologies in the writing process" section, placed before the References |
| **Format** | Structured statement describing the tool, how it was used, and human oversight |
| **Authorship** | AI cannot be listed as author or co-author |
| **Image policy** | AI-generated images are not permitted unless AI is part of the research methodology |
| **Peer review** | AI tools must not be used by reviewers to process manuscripts |
| **Data policy** | AI-generated data must be clearly labeled; authors responsible for accuracy |
| **Exemptions** | Basic tools (grammar checkers, reference managers) may not require disclosure — check journal guidelines |
| **Template** | See `templates/ai-disclosure-elsevier.md` |

**Example Elsevier disclosure**:
> "During the preparation of this work the author(s) used [AI TOOL NAME] in order to [REASON]. After using this tool/service, the author(s) reviewed and edited the content as needed and take(s) full responsibility for the content of the publication."

### Springer Nature

| Requirement | Details |
|---|---|
| **Disclosure location** | Methods section or Acknowledgements (depends on journal) |
| **Format** | Description of AI tool, version, how it was used, and verification steps |
| **Authorship** | AI tools cannot be credited as authors; must meet ICMJE criteria |
| **Image policy** | AI-generated images not permitted for non-research purposes; research use must be disclosed in Methods |
| **Peer review** | Reviewers and editors must not upload manuscripts to generative AI tools |
| **Data policy** | AI-generated or AI-analyzed data must be disclosed with methodology |
| **Exemptions** | Standard spell-checkers and grammar tools typically exempt |
| **Template** | See `templates/ai-disclosure-springer.md` |

**Example Springer Nature disclosure**:
> "The authors declare that [AI TOOL with version] was used during the preparation of this manuscript for [specific purpose]. The authors reviewed, edited, and take full responsibility for the content."

### Wiley

| Requirement | Details |
|---|---|
| **Disclosure location** | Acknowledgements section or dedicated AI disclosure section (journal-dependent) |
| **Format** | Specific statement identifying tools used and how |
| **Authorship** | AI cannot meet authorship criteria; not permitted as author |
| **Image policy** | AI-generated images require explicit disclosure; not permitted in some journals |
| **Peer review** | Reviewers must not use AI to process confidential manuscripts |
| **Data policy** | Full disclosure of AI in data analysis required |
| **Exemptions** | Standard editing tools (spell-check, grammar) typically exempt |
| **Template** | See `templates/ai-disclosure-wiley.md` |

### Taylor & Francis

| Requirement | Details |
|---|---|
| **Disclosure location** | Separate AI disclosure statement (submitted during manuscript submission process) |
| **Format** | Structured statement per T&F template |
| **Authorship** | AI technologies cannot be listed as authors |
| **Image policy** | AI-generated images must be disclosed; restrictions vary by journal |
| **Peer review** | AI must not be used to process manuscripts under review |
| **Data policy** | AI in data collection/analysis must be described in Methods |
| **Exemptions** | Basic writing aids (spell-check) typically exempt |
| **Template** | See `templates/ai-disclosure-taylor-francis.md` |

### SAGE

| Requirement | Details |
|---|---|
| **Disclosure location** | Acknowledgements or Methods section (journal-dependent) |
| **Format** | Clear statement of AI tools used and purposes |
| **Authorship** | AI cannot be an author; all authors must be human |
| **Image policy** | AI-generated images require disclosure and justification |
| **Peer review** | Confidentiality must be maintained; no manuscript content to AI tools |
| **Data policy** | AI in analysis must be disclosed with methodology details |
| **Exemptions** | Grammar and spell-checking tools typically exempt |
| **Template** | See `templates/ai-disclosure-sage.md` |

---

## Journal-Specific Variations

Some journals have requirements beyond their publisher's standard policy:

### The Lancet (Elsevier)

- Requires AI disclosure in **both** the cover letter and the manuscript
- Requires identification of which sections used AI assistance
- Particularly strict on AI involvement in systematic reviews and meta-analyses
- Requires statement that no patient data was processed by AI tools

### Cell (Elsevier)

- Requires disclosure per Elsevier standard plus additional detail on computational methods
- AI-assisted code must be disclosed with specific tool and version
- Requires reproducibility statement for AI-assisted analyses

### Nature (Springer Nature)

- Requires disclosure in Methods section specifically
- AI-generated text must be clearly attributed
- Research involving AI-generated images requires specific ethics review

### BMJ

- Requires AI disclosure in the transparency declaration
- Specific requirement to describe AI's role at each stage of manuscript preparation
- Additional requirements for AI in clinical decision support research

### JAMA (AMA)

- Requires detailed AI disclosure in Methods
- Authors must describe specific prompts used (where applicable)
- Requires statement on data privacy and AI tool terms of service

### PLOS ONE

- Requires AI disclosure in cover letter and manuscript
- AI tools must be listed in Methods with version numbers
- Additional requirements for AI in systematic reviews (see PRISMA-S)

---

## Disclosure Decision Tree

```
Did you use ANY AI tool during manuscript preparation?
│
├── NO → No AI disclosure needed (but consider basic tools)
│
└── YES → What type of AI tool?
    │
    ├── Basic grammar/spell-check → Usually exempt, check journal guidelines
    │
    ├── Language editing/polishing → Disclose in Acknowledgements/designated section
    │
    ├── Content generation (drafting) → Disclose with specifics: tool, version, sections, oversight
    │
    ├── Literature search → Disclose in Methods; verify all results manually
    │
    ├── Data analysis → Disclose in Methods with full methodology
    │
    ├── Code generation → Disclose in Methods; include tool and version
    │
    ├── Image creation → Disclose; check if permitted by journal
    │
    └── Translation → Disclose; note human review by native speaker
```

---

## Required Disclosure Elements

A complete AI disclosure statement should include:

1. **Tool identification**: Name and version of AI tool(s) used (e.g., "ChatGPT-4, OpenAI, March 2025 version")
2. **Purpose**: Specific purpose for which AI was used (e.g., "language editing", "literature search", "statistical code generation")
3. **Scope**: Which sections or portions of the manuscript involved AI assistance
4. **Human oversight**: Statement confirming human review, editing, and verification of all AI-generated content
5. **Accountability**: Statement that authors take full responsibility for the content
6. **Data privacy**: Confirmation that no confidential or patient data was processed by AI tools (if applicable)

---

## Compliance Checking Procedure

Before submission, verify:

1. [ ] Identify the target journal and publisher
2. [ ] Check `config/publisher-policies.yaml` for base requirements
3. [ ] Check journal-specific author guidelines for additional requirements
4. [ ] Draft disclosure statement using appropriate template from `templates/`
5. [ ] Ensure disclosure covers ALL AI tools used (not just the most prominent one)
6. [ ] Place disclosure in the correct manuscript location per publisher requirements
7. [ ] Include disclosure in cover letter if required by journal
8. [ ] Verify statement specificity (tool name, version, purpose, sections)
9. [ ] Confirm all co-authors are aware of and agree with the disclosure
10. [ ] STOP gate: Human author reviews and approves final disclosure before submission

---

## Common Mistakes

1. **Vague disclosure**: "AI was used in preparing this manuscript" — too vague for most publishers
2. **Missing tool version**: "ChatGPT was used" — which version? GPT-3.5? GPT-4? When?
3. **Wrong location**: Placing disclosure in Acknowledgements when the publisher requires a dedicated section
4. **Incomplete scope**: Disclosing AI use for writing but not for literature search or data analysis
5. **Missing from cover letter**: Some journals require AI disclosure in the cover letter as well
6. **Not disclosing all tools**: Using multiple AI tools but only disclosing one
7. **Failing to update**: Revising a manuscript with AI assistance but not updating the disclosure statement
