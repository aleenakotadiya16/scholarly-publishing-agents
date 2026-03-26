# Skill: Image Integrity

## Description

Detects potential image manipulation, duplication, and splicing in manuscript figures. Uses perceptual hashing, pixel-level analysis, and metadata examination to identify images that may have been fabricated, duplicated, or improperly modified.

## When to Use

- During peer review integrity screening (Workflow 04)
- When flagged by editors during triage
- For systematic integrity audits

## Inputs

| Input | Type | Required | Description |
|---|---|---|---|
| `figures` | List of images | Yes | All manuscript figures |
| `figure_legends` | List of strings | Optional | Figure captions for context |
| `manuscript_text` | Text | Optional | Text referencing figures |

## Outputs

| Output | Type | Description |
|---|---|---|
| `integrity_report` | Object | Per-figure assessment |
| `duplication_pairs` | List | Pairs of potentially duplicated regions |
| `manipulation_indicators` | List | Specific manipulation concerns |
| `metadata_analysis` | Object | EXIF/metadata findings |
| `overall_assessment` | String | clean / flags_found / escalate |

## Step-by-Step Procedure

### Step 1: Metadata Analysis

For each figure file:
- Extract EXIF data (creation date, modification date, software used)
- Check for metadata stripping (may indicate manipulation)
- Identify creation software (Photoshop, ImageJ, PowerPoint, etc.)
- Note any metadata inconsistencies across figures

### Step 2: Duplication Detection

#### Within-Figure Duplication
- Divide figure into regions
- Compute perceptual hashes for each region
- Compare regions for high similarity (accounting for rotation, scaling, mirroring)
- Flag regions with similarity above threshold

#### Between-Figure Duplication
- Compare all figure pairs using perceptual hashing
- Account for legitimate reuse (e.g., same baseline image in a series)
- Flag unexpected duplication across different experimental conditions

### Step 3: Manipulation Indicator Analysis

| Indicator | Method | Concern Level |
|---|---|---|
| **Copy-move** | Block matching, SIFT keypoint analysis | High |
| **Splicing** | Error Level Analysis (ELA) | High |
| **Enhancement** | Histogram analysis, contrast discontinuities | Medium |
| **Background uniformity** | Noise pattern analysis | Medium |
| **Resolution mixing** | DPI/resolution analysis across regions | Medium |
| **Edge artifacts** | Boundary analysis at suspected splice points | High |

### Step 4: Contextual Assessment

Consider legitimate reasons for similar-looking figures:
- **Western blots**: Bands may look similar across conditions
- **Microscopy**: Similar cell types may appear similar
- **Time series**: Sequential images may share background
- **Control images**: Same control used across experiments is normal

### Step 5: Generate Report

```markdown
## Image Integrity Report

### Figures Analyzed: 5

### Figure 1: ✅ CLEAN
- Type: Bar chart (data visualization)
- Metadata: Created in R, consistent dates
- Duplication: None detected
- Manipulation: N/A (data-generated figure)

### Figure 2: ⚠️ FLAG
- Type: Western blot
- Metadata: Photoshop CS6, created 2025-06-15
- Duplication: Region in Lane 3 shows 87% similarity to Lane 5
- Manipulation: ELA shows inconsistent error levels in Lane 3
- Assessment: Recommend expert review
- Confidence: Medium
- NOTE: This could be a legitimate similar result or a duplicated band

### Figure 3: ✅ CLEAN
- Type: Microscopy image (H&E staining)
- Metadata: ImageJ, consistent dates
- Duplication: None detected across panels
- Manipulation: No indicators

### Overall Assessment: FLAGS FOUND
- 1 figure flagged for expert review (Figure 2)
- Recommend: Editor reviews Figure 2 with domain expert before proceeding
```

## Quality Criteria

| Criterion | Standard |
|---|---|
| False positive rate | Must be clearly communicated; aim for < 15% |
| True positive detection | Catches copy-move with > 80% accuracy |
| Contextual awareness | Distinguishes legitimate similarity from manipulation |
| Reporting tone | Flags, never accuses |

## Cross-References

- Workflows: `workflows/04-peer-review/integrity-screening.md`
- Agents: Integrity Agent
- Rules: `rules/quality-gates.md` (STOP-07 for confirmed concerns)
- Context: Hindawi/Wiley paper mill detection, Bik et al. image manipulation studies
- Tools: Forensically, FotoForensics, ImageTwin, Proofig
