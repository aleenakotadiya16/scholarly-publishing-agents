# Example: Editor Workflow

## Scenario

A journal editor receives a batch of new submissions and needs to triage them efficiently, match reviewers, and manage the review process. The journal is PLOS Digital Health, which receives high submission volumes.

---

## Workflow Trace

### Stage 1: Manuscript Triage (Workflow 04)

**User**: "I have 5 new submissions to triage. Help me screen them efficiently."

**Orchestrator Agent** → Routes to **Editor Agent**

**Editor Agent Actions**:

1. **Reads rules**: `rules/confidentiality.md`, `rules/quality-gates.md`

2. **Triage — Manuscript MS-2026-0087**:

   **Editor Agent** runs triage on each submission using `workflows/04-peer-review/editor-triage.md`:

   ```markdown
   ## Triage Report: MS-2026-0087

   **Title**: "Machine Learning for Predicting Hospital Readmissions"
   **Authors**: Chen, L.; Park, S.; Williams, R.
   **Article type**: Original Research
   **Submitted**: 2026-01-18

   ### Scope: ✅ In Scope
   Digital health + ML application — fits journal scope well.

   ### Quality: ✅ Acceptable
   - Structure: Complete IMRAD
   - Abstract: Structured, 248/300 words
   - Methods: Detailed, reproducible
   - References: 52 (appropriate)

   ### Integrity Pre-Screen: ⚠️ FLAGS FOUND
   - Tortured phrases detected:
     - "deep learning" → "profound learning" (Page 4, Line 78)
     - "random forest" → "arbitrary woodland" (Page 5, Line 112)
   - Recommendation: Escalate to Level 2 integrity screening

   ### COI: ✅ No Flags
   - No co-authorship between editor and authors (checked CrossRef)

   ### Recommendation
   **Hold for integrity screening** before sending to review
   ```

   **Editor Agent** → Invokes **Integrity Agent** for Level 2 screening:

   ```markdown
   ## Level 2 Integrity Screening: MS-2026-0087

   ### Paper Mill Indicators: ⚠️ CONCERN
   - Tortured phrases: 4 detected (high count)
     - "profound learning" (deep learning)
     - "arbitrary woodland" (random forest)
     - "highlight extraction" (feature extraction)
     - "strategic regression" (logistic regression)
   - Template pattern: Structure matches known paper mill template (72% similarity)
   - Author profile: Authors have no prior publications in digital health
   - Email: Non-institutional Gmail addresses for all authors

   ### Statistical Integrity: ⚠️
   - GRIM test: 2 failures (Table 2, means inconsistent with N)
   - Unusual: All p-values between 0.01-0.04 (suspicious clustering)

   ### OVERALL: CONCERN — RECOMMEND ESCALATION (STOP-07)
   Multiple paper mill indicators detected.
   Recommend editor review with integrity officer.
   ```

   **STOP-07** 🛑: Escalated to editor + integrity officer
   → Editor decides to desk reject with notification to integrity committee

3. **Triage — Manuscript MS-2026-0088**:

   ```markdown
   ## Triage Report: MS-2026-0088

   **Title**: "Patient Perspectives on Wearable Health Monitoring"
   **Authors**: Kumar, A.; Johnson, M.; O'Brien, T.
   **Article type**: Qualitative Research
   **Submitted**: 2026-01-19

   ### Scope: ✅ In Scope
   ### Quality: ✅ Acceptable
   ### Integrity Pre-Screen: ✅ Clear
   - No tortured phrases
   - Author profiles verified (established researchers)
   - Institutional emails
   ### COI: ✅ No Flags

   ### Recommendation
   **Send to peer review** ✅
   ```

   **STOP-06** 🛑: Editor approves → Send to review → CLEARED ✅

### Stage 2: Reviewer Matching (Workflow 04)

For MS-2026-0088, **Editor Agent** proceeds to reviewer matching (`workflows/04-peer-review/reviewer-matching.md`):

4. **Reviewer Search**:

   ```markdown
   ## Suggested Reviewers: MS-2026-0088

   ### Tier 1: Strong Match
   1. **Dr. Sarah Chen**, University of Sydney
      - Expertise: Qualitative health research, patient experience, wearables (88% match)
      - Publications: 12 papers on patient perspectives in digital health
      - COI: None detected ✅
      - Last review for journal: 3 months ago (available)

   2. **Prof. Maria Garcia**, King's College London
      - Expertise: Health technology assessment, qualitative methods (85% match)
      - Publications: 8 papers on wearable health technologies
      - COI: None detected ✅
      - Last review for journal: 6 months ago (available)

   3. **Dr. James Wilson**, University of Toronto
      - Expertise: mHealth, patient engagement, mixed methods (80% match)
      - Publications: 6 papers on patient perspectives in digital health
      - COI: None detected ✅
      - New to this journal's reviewer pool

   ### Tier 2: Good Match (Backup)
   4. **Dr. Yuki Tanaka**, University of Tokyo (75% match)
   5. **Dr. Emma Brown**, University of Melbourne (72% match)

   ### Excluded
   - Dr. Alex Thompson, Flinders University — same institution as Author 3
   - Dr. Lisa Wang, Stanford — co-authored with Author 1 in 2025

   ### Diversity Assessment
   - Geographic: Australia, UK, Canada, Japan, Australia
   - Gender: 3F, 2M
   - Career stage: 1 professor, 2 senior lecturers, 2 postdocs
   ```

   **STOP-06** 🛑: Editor selects reviewers → Approves Dr. Chen, Prof. Garcia, and Dr. Wilson → CLEARED ✅

### Stage 3: Decision Support

After reviews are received (8 weeks later):

5. **Decision Support**:

   ```markdown
   ## Editorial Decision Support: MS-2026-0088

   **Reviews received**: 3/3
   **Review period**: 6 weeks (within target)

   ### Reviewer Summary

   | | Dr. Chen | Prof. Garcia | Dr. Wilson |
   |---|---|---|---|
   | Recommendation | Minor revisions | Minor revisions | Major revisions |
   | Methodology | Sound | Sound | Minor concerns |
   | Significance | High | High | Moderate |
   | Presentation | Good | Very good | Good |

   ### Consensus Points
   - All agree the topic is important and timely
   - All appreciate the rigorous qualitative methodology (thematic analysis)
   - All request additional detail on participant recruitment

   ### Divergent Points
   - Dr. Wilson suggests additional theoretical framework (Reviewer 3)
     - Reviewers 1 and 2 feel current approach is adequate
   - Prof. Garcia suggests more context on wearable devices used
     - Others did not flag this

   ### Unresolved Issues
   - Transferability to non-English-speaking populations (raised by Dr. Wilson)
   - Sample diversity (predominantly urban; raised by Dr. Chen)

   ### Options for Editor
   1. **Minor revisions** (align with majority): Address recruitment details,
      sample diversity discussion, transferability limitations
   2. **Major revisions** (align with Dr. Wilson): Additionally require
      theoretical framework addition
   3. **Reject**: Not recommended given positive reviewer consensus

   **Recommendation**: Minor revisions appears most consistent with
   reviewer consensus. The theoretical framework suggestion could be
   addressed as an expanded discussion point without restructuring the paper.

   **AWAITING EDITOR DECISION (STOP-06)** 🛑
   ```

   **Editor**: Decides on minor revisions. Reviews and edits the decision letter drafted by the Editor Agent. → STOP-06 CLEARED ✅

---

## Audit Trail Summary

| Timestamp | Agent | Action | Gate |
|---|---|---|---|
| 2026-01-18 09:00 | Editor Agent | Triage MS-2026-0087 | — |
| 2026-01-18 09:15 | Integrity Agent | Level 2 screening MS-0087 | STOP-07 ⏳ |
| 2026-01-18 10:00 | Human (Editor) | Desk reject MS-0087 (paper mill) | STOP-07 ✅ |
| 2026-01-19 09:00 | Editor Agent | Triage MS-2026-0088 | STOP-06 ⏳ |
| 2026-01-19 09:30 | Human (Editor) | Send to review | STOP-06 ✅ |
| 2026-01-19 10:00 | Editor Agent | Reviewer matching | — |
| 2026-01-19 10:30 | Human (Editor) | Select 3 reviewers | STOP-06 ✅ |
| 2026-01-19 11:00 | Editor Agent | Invite reviewers | — |
| 2026-03-02 14:00 | Editor Agent | 3/3 reviews received | — |
| 2026-03-02 14:30 | Editor Agent | Decision support generated | STOP-06 ⏳ |
| 2026-03-02 16:00 | Human (Editor) | Decision: minor revisions | STOP-06 ✅ |

---

## Key Principles Demonstrated

1. **Paper mill detection works**: Tortured phrases and statistical anomalies caught a suspicious submission
2. **Human makes all decisions**: AI triages and recommends; editor decides
3. **COI screening is systematic**: Automated checks against publication databases
4. **Reviewer diversity**: Geographic, gender, and career stage diversity considered
5. **Decision support, not decisions**: Editor Agent summarizes and suggests; editor retains full authority
6. **Confidentiality maintained**: Reviewer identities protected; manuscript content not transmitted externally
