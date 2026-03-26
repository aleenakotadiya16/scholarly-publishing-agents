# Revision Tracking

## Purpose

Maintain a comprehensive record of all changes made during the revision process, enabling clear communication with reviewers and editors about what was modified, added, or removed.

---

## Change Documentation

### Change Log Format

```yaml
revision_log:
  manuscript_id: "MS-2026-0042"
  revision_round: 1
  revision_date: "2026-03-15"
  previous_version: "v1.0-submitted-2026-01-20"
  current_version: "v2.0-revised-2026-03-15"

  changes:
    - id: "R1-C1"
      reviewer: "Reviewer 1"
      comment: "Add sensitivity analysis for discount rate"
      response_type: "agree_and_revise"
      changes_made:
        - location: "Page 15, Lines 312-320"
          description: "Added sensitivity analysis paragraph"
          type: "addition"
        - location: "Supplementary Table S3"
          description: "New supplementary table with sensitivity results"
          type: "new_file"
      new_references_added: []
      
    - id: "R2-C3"
      reviewer: "Reviewer 2"
      comment: "The discussion is too long"
      response_type: "agree_and_revise"
      changes_made:
        - location: "Pages 16-19"
          description: "Reduced discussion from 1,200 to 900 words"
          type: "reduction"
      new_references_added: []
```

### Version Comparison

Produce two manuscript versions:
1. **Clean version**: Final revised manuscript without tracked changes
2. **Tracked changes version**: All modifications visible (insertions, deletions, moves)

### Summary of Changes

For the resubmission:

```markdown
## Summary of Revisions

### Major Changes
1. Added sensitivity analysis for discount rate (Reviewer 1, Comment 1)
2. Added stratified analysis by urban/rural setting (Reviewer 2, Comment 2)
3. Expanded limitations section (Reviewer 1, Comment 4)

### Minor Changes
1. Corrected reference #12 (Reviewer 1, Comment 6)
2. Improved Figure 2 resolution (Reviewer 2, Comment 5)
3. Added abbreviation definitions (Editor comment)

### New Content
- Supplementary Table S3 (sensitivity analysis results)
- 2 new references added (verified against CrossRef)

### Word Count Changes
- Previous: 3,450 words
- Current: 3,620 words (+170 words)
- Limit: 4,000 words ✅
```

---

## Best Practices

1. **Number every change** and link it to the reviewer comment that triggered it
2. **Record page and line numbers** for both tracked-changes and clean versions
3. **Track new references** separately for re-verification
4. **Note changes not requested by reviewers** (e.g., author-initiated improvements)
5. **Maintain version history** in case of multiple revision rounds
6. **Update metadata** (word count, figure count, reference count) after each revision
