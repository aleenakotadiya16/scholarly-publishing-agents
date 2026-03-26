# Workflow 07: Post-Publication

## Overview

Post-publication activities including impact tracking, erratum/corrigendum management, and dissemination of research findings to broader audiences.

**Primary Agent**: Production Agent, Author Agent
**Quality Gates**: STOP-10 (erratum/corrigendum publication)

---

## Workflow Diagram

```mermaid
graph TD
    A[Published Article] --> B{Post-Publication Activity?}
    B -->|Impact Tracking| C[Impact Monitoring]
    B -->|Error Found| D[Error Assessment]
    B -->|Dissemination| E[Dissemination Activities]

    C --> C1[Citation Tracking]
    C1 --> C2[Altmetric Monitoring]
    C2 --> C3[Media Coverage Tracking]
    C3 --> C4[Usage Statistics]
    C4 --> C5[Generate Impact Report]

    D --> D1{Error Severity?}
    D1 -->|Minor - Erratum| D2[Draft Erratum Notice]
    D1 -->|Significant - Corrigendum| D3[Draft Corrigendum]
    D1 -->|Fundamental - Retraction| D4[Retraction Process]
    D2 --> D5{STOP-10: All Authors Approve}
    D3 --> D5
    D4 --> D6[Contact Editor - Separate Process]
    D5 -->|Approved| D7[Submit Correction to Journal]

    E --> E1[Plain-Language Summary]
    E1 --> E2[Social Media Posts]
    E2 --> E3[Policy Brief - if applicable]
    E3 --> E4[Press Release - if applicable]
    E4 --> E5[Repository/Archive Deposit]
```

---

## Steps

### Step 1: Impact Tracking
See: `impact-tracking.md`

Monitor and report on article impact through citations, Altmetric scores, media mentions, and usage statistics.

### Step 2: Erratum/Corrigendum Management
See: `erratum-corrigendum.md`

Handle post-publication corrections, from error identification through correction notice publication. Includes STOP-10 gate for author approval.

### Step 3: Dissemination
See: `dissemination.md`

Create plain-language summaries, social media content, policy briefs, and other materials to maximize research impact and reach non-academic audiences.

---

## Sub-Files

| File | Purpose |
|---|---|
| `impact-tracking.md` | Citation and altmetric monitoring |
| `erratum-corrigendum.md` | Post-publication corrections |
| `dissemination.md` | Plain-language summaries and outreach |
