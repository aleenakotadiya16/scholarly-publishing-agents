# Integrity Screening

## Purpose

Comprehensive research integrity screening for manuscripts, covering paper mill detection, image forensics, statistical consistency, and citation analysis. This is the Integrity Agent's primary workflow.

---

## Screening Components

### 1. Paper Mill Detection

Paper mills mass-produce fabricated studies for sale. Indicators include:

#### Tortured Phrases
Paper mills often use synonym substitution to evade plagiarism detection, producing "tortured phrases":

| Expression | Tortured Version |
|---|---|
| Artificial intelligence | Counterfeit knowledge |
| Signal-to-noise ratio | commotion/resonance proportion |
| Breast cancer | bosoms growth |
| Random forest | irregular backwoods |
| Deep learning | profound learning |
| Logistic regression | strategic regression |
| Feature extraction | highlight extraction |
| Neural network | brain organization |
| Cloud computing | distributed computing |
| Blockchain | chain square |

**Detection method**: NLP-based pattern matching for unusual synonym substitutions in technical contexts.

#### Metadata Patterns
| Pattern | Detection |
|---|---|
| **Identical submission timelines** | Multiple papers submitted within hours |
| **Template structure** | Nearly identical structure across unrelated papers |
| **Author name patterns** | Chinese names transliterated identically across mills |
| **Affiliation mismatches** | Hospital authors writing on unrelated CS topics |
| **Email patterns** | Non-institutional emails from supposedly academic authors |
| **Suggesting own reviewers** | Suggested reviewers are fake or compromised accounts |

#### Reference Context: Wiley/Hindawi

In 2023-2024, Wiley retracted over 11,300 papers from Hindawi journals due to paper mill activity, resulting in an $18M revenue impact. The paper mill operation involved:
- Compromised special issue guest editors
- Fabricated peer reviews
- Mass-produced papers with manipulated data
- Citation rings to boost metrics

### 2. Image Forensics

#### Duplication Detection
- **Copy-move detection**: Search for identical regions within or across figures
- **Perceptual hashing**: Identify visually similar images that may be rotated, scaled, or cropped versions of the same source
- **Metadata analysis**: Check EXIF data for creation dates, software used, modification history

#### Manipulation Indicators
| Indicator | Concern |
|---|---|
| **Identical background noise** | Different experimental conditions showing identical noise patterns |
| **Cloned regions** | Copy-pasted areas within blots, microscopy images |
| **Splicing artifacts** | Brightness/contrast discontinuities at region boundaries |
| **Resolution inconsistencies** | Mixed resolutions within a single figure |
| **Missing raw data** | Original unprocessed images not available |

#### Tools
- Forensically (browser-based image forensics)
- FotoForensics (ELA analysis)
- ImageTwin (automated scientific image screening)
- Proofig (commercial scientific image integrity)

### 3. Statistical Integrity

#### GRIM Test (Granularity-Related Inconsistency of Means)
For studies reporting means of integer-based data (e.g., Likert scales):
- Calculate whether the reported mean is mathematically possible given the sample size
- Example: A mean of 3.47 with n=20 on a 1-5 scale is impossible (20 × 3.47 = 69.4, not an integer)

#### SPRITE Test (Sample Parameter Reconstruction via Iterative TEchniques)
Extension of GRIM:
- Reconstruct possible datasets that could produce the reported summary statistics
- If no valid dataset exists, the statistics may be fabricated

#### P-Value Distribution
- Natural p-values cluster just below significance thresholds — but not TOO consistently
- Suspicious pattern: All reported p-values are 0.04-0.049 (suggests p-hacking or fabrication)
- Expected pattern: Mix of significant and non-significant results in honest research

#### Other Statistical Checks
| Check | Purpose |
|---|---|
| **Effect size plausibility** | Are effect sizes within reasonable bounds for the field? |
| **Sample size vs. claims** | Can this sample size detect the reported effect? (power analysis) |
| **Standard deviation** | Are SDs reasonable for the data type? (impossible SDs for bounded data) |
| **Rounding consistency** | Are all values rounded to the same decimal places? |
| **Decimal consistency** | Do reported values match re-calculated values from tables? |

### 4. Citation Network Analysis

| Pattern | Concern |
|---|---|
| **Citation rings** | Group of papers that cite each other circularly |
| **Coercive citation** | Editor or reviewer pressuring citation of specific papers |
| **Excessive self-citation** | > 15% of references are self-citations (WARN-04) |
| **Review journal padding** | Citing low-quality review articles for breadth |
| **Retracted paper citation** | Citing papers that have been retracted |

### 5. Authorship Concerns

| Pattern | Concern |
|---|---|
| **Gift/guest authorship** | Authors who didn't contribute substantively |
| **Ghost authorship** | Contributors not listed as authors |
| **Authorship for sale** | Paper mill "author slot" purchasing |
| **Rapid publication rate** | Author publishing at an implausible rate |

---

## Integrity Report Format

```markdown
## Integrity Screening Report

**Manuscript**: [MS-ID]
**Date**: [Date]
**Screening level**: [Basic / Standard / Comprehensive]

### Overall Assessment: [CLEAR / FLAGS FOUND / CONCERN RAISED]

### Paper Mill Indicators
- Tortured phrases: [None detected / List found]
- Template patterns: [None / Suspicious similarity to X]
- Metadata: [Normal / Flags: specify]

### Image Integrity
- Duplication: [None detected / Flagged figures: list]
- Manipulation indicators: [None / Flagged: specify]
- Note: [Automated screening only — expert review recommended for flagged items]

### Statistical Integrity
- GRIM test: [Pass / Fail on X values]
- P-value distribution: [Normal / Suspicious clustering]
- Effect sizes: [Plausible / Unusual]
- Internal consistency: [Consistent / Discrepancies found: specify]

### Citation Analysis
- Self-citation rate: [X%]
- Citation rings: [None detected / Suspicious pattern]
- Retracted citations: [None / Found: list]

### Recommendation
[Clear for review / Recommend additional screening / Escalate to integrity officer]
```

---

## Escalation Protocol (STOP-07)

If any screening component raises a concern:
1. Document the specific finding with evidence
2. Assess severity (low / medium / high / critical)
3. Trigger STOP-07: present findings to a qualified human (editor, integrity officer)
4. **NEVER publicly flag an integrity concern** — false accusations damage careers
5. The human decides next steps (request clarification from authors, additional screening, reject, or investigate)
