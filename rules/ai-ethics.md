# AI Ethics Rules for Scholarly Publishing

## Authority

These rules are derived from:
- **COPE (Committee on Publication Ethics)** position statement on AI in scholarly publishing (2023, updated 2024)
- **ICMJE** recommendations on AI-assisted authorship
- Publisher-specific policies from Elsevier, Springer Nature, Wiley, Taylor & Francis, and SAGE
- **World Association of Medical Editors (WAME)** guidelines on ChatGPT and AI

---

## The Three Pillars

### Pillar 1: Human Accountability

**Every aspect of a published work must have a human who is accountable for it.**

- AI tools cannot be listed as authors on manuscripts. COPE is explicit: "AI tools cannot meet the requirements for authorship as they cannot take responsibility for the submitted work."
- At least one human author must take full responsibility for the integrity of the entire work — including any content generated or assisted by AI.
- The corresponding author must be able to explain, defend, and take responsibility for all content, including AI-assisted portions.
- All co-authors must have reviewed and approved AI-assisted content.
- ICMJE authorship criteria (substantial contribution, drafting/revising, final approval, accountability) cannot be met by AI systems.

**Practical implication for agents**: Never produce content that suggests AI is an author. Always attribute responsibility to the human researcher.

### Pillar 2: Transparency

**All AI use in manuscript preparation must be disclosed.**

- Any use of AI tools (including large language models, image generators, data analysis tools) must be disclosed in the manuscript.
- Disclosure must be specific — which tools were used, how they were used, and at which stages.
- "I used ChatGPT" is insufficient. Disclosure should specify: "ChatGPT-4 (OpenAI, March 2025 version) was used to assist with language editing of the Methods section. All AI-generated suggestions were reviewed, verified, and edited by [Author Name]."
- The location of disclosure varies by publisher (see `rules/disclosure-compliance.md`).
- AI use in data analysis must be described in the Methods section.
- AI use in writing must be disclosed in the Acknowledgements or a separate AI declaration.

**Practical implication for agents**: Maintain a log of all AI-assisted activities during manuscript preparation. Generate publisher-appropriate disclosure statements.

### Pillar 3: Authorship Restrictions

**AI cannot be an author, funder, or reviewer.**

- AI tools cannot be listed in author bylines.
- AI tools cannot be cited as a source of original ideas or findings.
- AI cannot serve as a peer reviewer (confidentiality and accountability concerns).
- AI tools should not be listed as funding sources.
- AI assistance does not constitute a "contribution" under CRediT taxonomy.

**Practical implication for agents**: Never suggest listing AI as an author or contributor. When using CRediT roles, only assign roles to human authors.

---

## Publisher-Specific Ethics Positions

### Elsevier
- AI and AI-assisted technologies should not be listed as an author or co-author
- Authors must disclose AI use in their manuscript
- Authors are responsible and accountable for all content
- AI-generated images are prohibited unless AI is part of the research design
- AI must not be used in peer review processes

### Springer Nature
- AI tools cannot be credited as authors
- Use of AI must be disclosed in the Methods or Acknowledgements
- Authors bear full responsibility for accuracy of AI-generated content
- AI-generated images in non-research contexts are not permitted
- Large language models must not be used to process confidential peer review material

### Wiley
- AI cannot fulfill authorship criteria
- AI use must be disclosed with specific details
- Authors are accountable for verifying AI-generated content
- Context: Wiley/Hindawi retracted 11,300+ papers linked to paper mill activity — heightened vigilance on integrity

### Taylor & Francis
- AI tools cannot be authors
- Transparent disclosure of AI use required
- Human oversight and accountability mandatory
- Specific disclosure format provided by T&F

### SAGE
- AI cannot be an author
- Full disclosure of AI assistance required
- Authors must verify all AI-generated content
- SAGE provides specific guidance on acceptable vs. unacceptable AI use

---

## Prohibited Uses of AI in Scholarly Publishing

1. **Fabricating data or results** — AI must never be used to generate fake data, invent experimental results, or create false statistical outputs.
2. **Fabricating citations** — AI must never generate references that don't exist (see `rules/citation-integrity.md`).
3. **Ghostwriting without disclosure** — Using AI to write substantial portions of a manuscript without disclosure violates all major publisher policies.
4. **Processing confidential peer review materials** — Submitting manuscripts under review to AI tools breaches confidentiality (see `rules/confidentiality.md`).
5. **Generating misleading images** — Using AI to create or alter scientific images in ways that misrepresent data.
6. **Manipulating peer review** — Using AI to generate fake reviews, suggest fake reviewers, or manipulate the review process.
7. **Authorship fraud** — Listing AI as an author, or using AI to generate content for "guest" or "gift" authorship.

---

## Permitted Uses of AI (with Disclosure)

1. **Language editing and polishing** — Grammar, clarity, readability improvements (must disclose)
2. **Literature search assistance** — Using AI to identify relevant papers (must verify all results)
3. **Data analysis support** — Using AI tools for statistical analysis (must disclose in Methods, verify results)
4. **Figure preparation** — Using AI for data visualization (not image generation of scientific content)
5. **Formatting assistance** — Using AI to format manuscripts to journal requirements
6. **Translation** — Using AI for language translation (must disclose, must have native speaker review)
7. **Code generation** — Using AI to assist with research code (must disclose, must verify)

---

## Agent Compliance Checklist

Before completing any task, agents must verify:

- [ ] No AI-generated content is presented as original research findings
- [ ] All factual claims are traceable to verified sources
- [ ] AI involvement is documented for disclosure
- [ ] No confidential manuscript content is sent to external services
- [ ] Human accountability is maintained for all decisions
- [ ] All citations are verified (not fabricated)
- [ ] Content is clearly marked as AI-assisted vs. human-written
- [ ] Publisher-specific requirements are checked and followed

---

## Enforcement

- The **Integrity Agent** monitors compliance with these rules across all workflows
- The **Orchestrator Agent** enforces quality gates that include ethics checks
- Violations trigger STOP gates requiring human intervention
- All agent actions are logged for audit trail purposes
