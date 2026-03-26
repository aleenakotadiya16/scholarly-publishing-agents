# Editor Triage — Manuscript Screening

## Purpose

Assist editors in the initial screening of submitted manuscripts, helping with scope assessment, quality evaluation, and integrity flagging. The goal is to help editors make efficient triage decisions while ensuring nothing concerning is missed.

---

## Triage Screening Steps

### Step 1: Scope Check

Evaluate whether the manuscript falls within the journal's scope:

| Criterion | Assessment |
|---|---|
| **Discipline match** | Does the topic align with the journal's stated scope? |
| **Article type** | Does the journal accept this type of article? |
| **Methodology** | Is the methodology appropriate for this journal? |
| **Audience** | Is the target audience aligned with the journal's readership? |
| **Novelty** | Does it appear to contribute something new? |

**Output**: Scope assessment (In scope / Borderline / Out of scope)

### Step 2: Basic Quality Screen

Quick quality assessment:

| Criterion | Red Flags |
|---|---|
| **Structure** | Missing key sections (Methods, Results, etc.) |
| **Abstract** | Doesn't match journal requirements; claims not in paper |
| **Language** | Incomprehensible writing; excessive grammar errors |
| **Length** | Significantly over/under word limit |
| **References** | Too few, too old, or formatting completely wrong |
| **Figures/Tables** | Missing, low quality, or unreferenced |
| **Ethical statements** | Missing ethics approval, consent, or COI declaration |

**Output**: Quality assessment (Acceptable / Needs work / Below threshold)

### Step 3: Integrity Pre-Screen

Quick integrity flags (full screening in `integrity-screening.md`):

| Check | What to Look For |
|---|---|
| **Tortured phrases** | "counterfeit" for "sham", "intriguing" for "interesting" |
| **Template patterns** | Suspiciously formulaic structure matching paper mill templates |
| **Author profile** | Authors with no prior publications in the field; institutional email mismatch |
| **Citation patterns** | Excessive citation of a small group of authors/journals |
| **Too-good data** | Perfectly round numbers, impossibly large sample sizes |
| **Image concerns** | Visually similar panels, unusual artifacts |

**Output**: Integrity flag (Clear / Needs screening / Concern raised)

### Step 4: Conflict of Interest Check

Before assigning to an editor or sending to review:

1. Check handling editor for COI with authors
2. Check if any editorial board members are authors
3. Flag institutional conflicts
4. Check if similar work is under review at the journal

### Step 5: Triage Decision Support

Present a structured triage summary:

```markdown
## Triage Report

**Manuscript**: [MS-ID]
**Title**: [Title]
**Authors**: [Author list]
**Article type**: [Type]
**Submitted**: [Date]

### Scope: ✅ In Scope
[Brief explanation]

### Quality: ⚠️ Needs Attention
- Missing structured abstract (journal requirement)
- Reference list formatting does not match journal style
- Word count 4,500 (limit 4,000) — needs reduction

### Integrity: ✅ No Flags
- No tortured phrases detected
- Author profiles appear legitimate
- Citation patterns normal

### COI: ⚠️ Flag
- Author B is a former PhD student of Editor C (within 5 years)
- Recommendation: Assign to a different handling editor

### Recommendation
**Proceed to peer review** with note to authors about formatting issues
(Editor decision required — STOP-06)
```

---

## Decision Options

| Decision | When | Action |
|---|---|---|
| **Desk reject** | Out of scope, below quality threshold, serious integrity concern | STOP-06: Editor decision letter |
| **Return to author** | Minor fixable issues (formatting, missing declarations) | Request corrections before review |
| **Send to review** | In scope, acceptable quality, no integrity flags | Proceed to reviewer matching |
| **Escalate** | Integrity concern requiring investigation | STOP-07: Integrity escalation |

---

## Volume Management

For journals with high submission volumes:
- Prioritize by article type (e.g., registered reports, invited submissions)
- Use integrity pre-screening to quickly flag problematic submissions
- Batch similar topics for efficient editor assignment
- Track time-in-triage to maintain reasonable turnaround
