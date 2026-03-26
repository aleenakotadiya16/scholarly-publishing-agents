# Peer Review Confidentiality Rules

## Fundamental Principle

**Peer review is confidential.** This is a foundational principle of scholarly publishing, upheld by COPE, ICMJE, and every major publisher. Violations of peer review confidentiality can:

- Compromise the integrity of the review process
- Harm authors whose unpublished work is exposed
- Undermine trust in the publishing system
- Result in sanctions against reviewers and editors
- Have legal implications (breach of contract, intellectual property)

---

## Rules for AI Systems in Peer Review

### Rule 1: Never Feed Manuscripts to External AI Tools

**Manuscripts under peer review must NOT be uploaded, pasted, or otherwise transmitted to:**

- Large language model services (ChatGPT, Claude, Gemini, etc.)
- AI writing assistants
- Plagiarism detection services not authorized by the publisher
- Any cloud-based service that may store or use the content for training
- Any service where the data processing terms allow the provider to use uploaded content

**Why**: Uploading a manuscript to an AI service potentially:
- Exposes unpublished findings to the service provider
- Risks the manuscript content entering training data
- Violates the confidentiality agreement between reviewer and journal
- May constitute intellectual property theft

**Exception**: Publisher-approved screening tools operated within the publisher's infrastructure (e.g., iThenticate for plagiarism, publisher-specific integrity screening tools).

### Rule 2: Protect Author Identity

In single-blind and double-blind review:

- **Single-blind**: Reviewer knows authors, but reviewer identity is protected from authors. AI agents must NEVER reveal reviewer identity.
- **Double-blind**: Neither party knows the other's identity. AI agents must NOT attempt to identify authors from manuscript content (e.g., writing style analysis, citation patterns, institutional clues).
- **Triple-blind**: Neither party knows identities, and the editor doesn't know reviewer identities. Extremely rare but requires the strictest protections.

### Rule 3: Protect Manuscript Content

- NEVER store manuscript content beyond the immediate review session
- NEVER include manuscript excerpts in logs, error reports, or telemetry
- NEVER share manuscript content across agent contexts (i.e., a review of Manuscript A should not be accessible when reviewing Manuscript B)
- NEVER use manuscript content to train or fine-tune AI models

### Rule 4: Protect Review Content

- Reviewer comments are confidential to the editor and (where applicable) the author
- NEVER share one reviewer's comments with another reviewer (unless the journal operates open review)
- NEVER disclose review scores, recommendations, or editorial decisions before official communication
- NEVER use review content to train or fine-tune AI models

### Rule 5: Protect Editorial Decisions

- Accept/reject decisions are confidential until communicated through official channels
- Editorial discussions about manuscripts are confidential
- Editor-reviewer communications about specific manuscripts are confidential

---

## Conflict of Interest Detection

### Editor-Author Conflicts

AI agents supporting editors should flag potential conflicts of interest:

| Conflict Type | Detection Method | Action |
|---|---|---|
| **Co-authorship** | Check if editor and author have co-authored papers in the past 3-5 years | Flag for editorial office |
| **Institutional** | Check if editor and author share an institution or department | Flag for editorial office |
| **Funding** | Check if editor and author share funding sources | Flag for editorial office |
| **Personal relationship** | Cannot be detected by AI — rely on editor self-declaration | Remind editor of disclosure obligation |
| **Competitive** | Check if editor is working on similar research | Flag for editorial office |
| **Financial** | Cannot be reliably detected by AI | Remind editor of disclosure obligation |

### Reviewer-Author Conflicts

When suggesting reviewers, flag potential conflicts:

| Conflict Type | Detection Method |
|---|---|
| **Recent co-authorship** | Search PubMed/CrossRef for shared publications (past 3-5 years) |
| **Same institution** | Check affiliations |
| **Advisor-advisee** | Check acknowledgements sections and thesis databases |
| **Same grant** | Check funding statements in recent publications |
| **Frequent mutual citation** | Analyze citation networks for unusual mutual citation frequency |

### Reviewer-Reviewer Conflicts

- Check that multiple reviewers on the same manuscript don't share institutional or co-authorship ties
- Ensure diverse perspectives by selecting reviewers from different research groups

---

## Open Peer Review Exceptions

Some journals operate open peer review models where standard confidentiality rules are modified:

| Model | Confidentiality Rules |
|---|---|
| **Traditional (closed)** | Full confidentiality; all rules above apply |
| **Open identity** | Reviewer names disclosed to authors; manuscript content still confidential |
| **Open reports** | Reviews published alongside article; review content not confidential post-publication |
| **Open participation** | Community can comment; manuscript is effectively public during review |

**Always check the journal's review model before applying confidentiality rules.** The default assumption should be traditional closed review.

---

## Practical Guidelines for AI Agents

### When Assisting Reviewers

1. Work within the reviewer's local environment only — no external API calls with manuscript content
2. Process the manuscript in-session only — do not persist content
3. Generate structured review templates locally
4. Statistical checks can be performed on extracted numbers (not full text) using local tools
5. Literature searches for context are acceptable (searching for published papers related to the topic, not searching for the manuscript itself)

### When Assisting Editors

1. Screening tools should operate within the publisher's infrastructure
2. Conflict-of-interest checks use publicly available publication data (not manuscript content)
3. Reviewer matching uses expertise profiles and publication histories (public data)
4. Decision support summarizes review content locally — never transmits it externally

### When Assisting Authors

1. Authors CAN use AI tools on their own manuscripts (with disclosure)
2. But authors should NOT share reviewer comments or editor decision letters with AI tools unless the journal explicitly permits this
3. Response-to-reviewers letters can be drafted with AI assistance if reviewer comments are processed locally
4. Always disclose AI use in revision per publisher policy

---

## Breach Protocols

If a confidentiality breach is detected or suspected:

1. **STOP gate**: Immediately halt the current process
2. **Log the incident**: Record what data was exposed, when, and how
3. **Notify the editor/editorial office**: The breach must be reported to the journal
4. **Assess scope**: Determine what content was exposed and to whom
5. **Remediate**: Take steps to contain the breach (e.g., request deletion from external service)
6. **Document**: Create a full incident report for the editorial office

---

## Publisher-Specific Confidentiality Policies

### COPE Guidance
- Peer review confidentiality is a core ethical obligation
- Breaches should be investigated by the journal/publisher
- Sanctions may include banning from reviewer pools

### ICMJE
- Reviewers must treat manuscripts as confidential
- Must not use information from manuscripts for personal advantage
- Must not share manuscripts with others without editor permission

### All Major Publishers (Elsevier, Springer Nature, Wiley, T&F, SAGE)
- Explicitly prohibit uploading manuscripts to AI tools during review
- Require reviewers to agree to confidentiality terms
- Some are implementing technical controls to detect AI processing of manuscripts
