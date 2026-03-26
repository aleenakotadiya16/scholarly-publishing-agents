# Impact Tracking

## Purpose

Monitor and report on the impact of published research through citation metrics, altmetrics, media coverage, and usage statistics.

---

## Impact Metrics

### Citation Metrics

| Metric | Source | Description |
|---|---|---|
| **Citation count** | Google Scholar, Scopus, Web of Science, CrossRef | Number of papers citing this article |
| **Citation context** | Scite.ai | How the article is cited (supporting, contradicting, mentioning) |
| **h-index contribution** | Scopus, Google Scholar | Whether this paper contributes to the author's h-index |
| **Field-weighted citation impact** | SciVal/Scopus | Citations relative to field average |

### Altmetrics

| Source | What It Tracks |
|---|---|
| **Altmetric.com** | Aggregate altmetric attention score |
| **Twitter/X** | Social media mentions, retweets, engagement |
| **News** | Media coverage (Altmetric tracks 2,000+ news sources) |
| **Policy** | Mentions in policy documents (WHO, government agencies) |
| **Wikipedia** | Citations in Wikipedia articles |
| **Mendeley** | Reader counts (proxy for academic interest) |
| **Blog posts** | Discussion in science blogs |
| **Peer review** | Post-publication peer review (Publons, PubPeer) |

### Usage Statistics

| Metric | Source |
|---|---|
| **Abstract views** | Publisher platform |
| **Full-text downloads** | Publisher platform |
| **PDF downloads** | Publisher platform |
| **Geographic distribution** | Publisher platform (which countries are reading) |
| **Referral sources** | Publisher platform (how readers find the article) |

---

## Monitoring Schedule

| Period | Actions |
|---|---|
| **Week 1** | Check Altmetric score, social media mentions |
| **Month 1** | First citation check, usage statistics, media coverage |
| **Month 3** | Citation update, altmetric trends |
| **Month 6** | Comprehensive impact assessment |
| **Year 1** | Annual impact report |
| **Ongoing** | Google Scholar alerts for new citations |

---

## Impact Report Format

```markdown
## Impact Report

**Article**: [TITLE]
**DOI**: [DOI]
**Published**: [DATE]
**Report date**: [DATE]
**Time since publication**: [X months]

### Citation Metrics
- Google Scholar citations: XX
- Scopus citations: XX
- Web of Science citations: XX
- Notable citing papers: [list key papers that cited this work]

### Altmetric Score: XX
- Twitter/X: XX mentions
- News: XX outlets
- Blog: XX posts
- Policy: XX documents
- Wikipedia: XX citations
- Mendeley readers: XX

### Usage
- Abstract views: XX
- Full-text views: XX
- PDF downloads: XX
- Top countries: [list]

### Notable Impact
- [Cited in WHO guidelines]
- [Featured in The Conversation]
- [Referenced in government policy document]

### Recommendations
- Consider writing a follow-up commentary
- Engage with citing authors for collaboration
- Prepare a policy brief based on the findings
```

---

## Tools and APIs

| Tool | Purpose | Access |
|---|---|---|
| **Altmetric API** | Altmetric attention data | `https://api.altmetric.com/v1/doi/{DOI}` |
| **CrossRef Event Data** | Citation events | `https://api.eventdata.crossref.org/v1/events` |
| **Scopus API** | Citation metrics | Requires institutional access |
| **Google Scholar Alerts** | New citation notifications | Set up via Google Scholar |
| **Semantic Scholar** | Citation context | `https://api.semanticscholar.org/v1/paper/{DOI}` |
| **PlumX** | Comprehensive metrics | Via Elsevier/Scopus |

---

## Setting Up Monitoring

1. **Google Scholar alert**: Set up for the exact article title
2. **Altmetric bookmarklet**: Install for quick score checking
3. **ORCID profile**: Ensure the paper is linked to all authors' ORCID profiles
4. **Institutional repository**: Deposit the accepted manuscript (green OA) per publisher policy
5. **OSF**: Link the paper to the OSF project (if applicable)
6. **ResearchGate / Academia.edu**: Update profiles with the new publication
