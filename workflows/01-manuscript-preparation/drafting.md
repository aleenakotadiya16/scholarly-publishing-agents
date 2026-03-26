# AI-Assisted Drafting with Anti-Hallucination Guards

## Purpose

Guide AI-assisted manuscript drafting that maximizes writing quality while preventing hallucination, fabrication, and ethical violations.

---

## Principles

1. **The author provides substance; AI refines expression.** AI should never generate novel claims, findings, or data.
2. **Every factual statement must have a source.** Either the author's own research data or a verified citation.
3. **AI suggestions are drafts, not final text.** All AI output requires human review (STOP-01).
4. **Transparency is maintained.** Track which portions were AI-assisted for disclosure purposes.

---

## Section-Specific Guidance

### Title
- AI can suggest title variations based on the author's working title
- AI must NOT fabricate results or findings in the title
- Author chooses final title

### Abstract
- AI can structure the abstract per journal requirements (structured vs. unstructured)
- All claims in the abstract must be present in the full manuscript
- AI should check: does every abstract claim have a corresponding section in the paper?
- Word count must comply with journal limits (check `config/journal-requirements.yaml`)

### Introduction
- AI can help structure the argument (background → knowledge gap → rationale → objectives)
- All background claims must be cited with verified references
- AI must NOT overstate the novelty or significance of the work
- The research question/hypothesis must come from the author

### Methods
- AI can help with standardized descriptions (e.g., statistical methods language)
- AI must NEVER fabricate methodological details
- Study design, population, interventions, and outcomes must come from the author
- AI can check completeness against reporting guidelines (CONSORT, STROBE, PRISMA)
- Statistical methods should be precise and verifiable

### Results
- AI must NEVER generate, interpolate, or fabricate results data
- AI can help format results tables and structure the narrative
- AI can check consistency between text, tables, and figures
- All numbers must come from the author's data analysis
- AI can flag potential inconsistencies (e.g., percentages that don't add up)

### Discussion
- AI can help structure the discussion (summary → comparison with literature → implications → limitations → conclusion)
- All comparisons with existing literature must use verified citations
- AI can suggest connections to broader literature (but citations must be verified)
- AI must NOT overinterpret results or make unsupported causal claims
- Limitations should be comprehensive and honest

### References
- Every reference must pass citation verification (see `skills/citation-verification.md`)
- AI should NEVER generate references from memory
- Reference formatting must match journal style (check `config/journal-requirements.yaml`)

---

## Anti-Hallucination Checklist (Run After Each Section)

For each paragraph of AI-assisted text, verify:

1. [ ] Does every factual claim have a citation or refer to the author's own data?
2. [ ] Are all cited references verified against CrossRef/PubMed/DOI?
3. [ ] Are all statistics traceable to the author's data or cited sources?
4. [ ] Does the text accurately represent what cited sources actually say?
5. [ ] Are there any claims that "sound right" but lack evidence?
6. [ ] Is there any text that the author cannot explain or defend?
7. [ ] Are comparative statements (e.g., "larger than previous studies") verifiable?

---

## AI Assistance Tracking

Maintain a log of AI involvement for disclosure purposes:

```yaml
ai_assistance_log:
  tool: "Claude (Anthropic, 2025)"
  sections_assisted:
    - section: "Introduction"
      type: "language editing and structure"
      description: "AI assisted with structuring the literature background and improving clarity"
    - section: "Methods"
      type: "standardized language"
      description: "AI helped with standardized statistical methods descriptions"
    - section: "Discussion"
      type: "structure and language"
      description: "AI helped organize discussion structure and improve readability"
  sections_not_assisted:
    - "Results (all content from author's data analysis)"
    - "Figures and tables (created by author)"
  human_oversight: "All AI-assisted text reviewed and edited by all authors"
```

---

## Red Flags During Drafting

Stop and alert the author if:

- The AI is generating specific statistics or numbers not provided by the author
- The AI is creating references it hasn't verified
- The AI is making causal claims from correlational data
- The AI is overstating significance or novelty
- The AI is generating content the author hasn't directed or couldn't verify
- The AI is inserting hedging language that obscures honest uncertainty
- The AI is generating methods details the author hasn't specified
