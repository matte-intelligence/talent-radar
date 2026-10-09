# Talent Radar — evaluation plan

**Version:** 0.9 (public). We publish metrics only when measured; until then,
this page is the definition — not the result.

## Metrics

| # | Metric | Definition | Baseline | Target (prototype) |
|---|---|---|---|---|
| 1 | **Source accuracy** | % of evidence items whose claim matches its cited source on human audit (sample 50/mandate) | TBD (manual research audit, parent-firm practice) | ≥ 95 % |
| 2 | **Research time** | total wall-clock from mandate brief to review-ready profiles | manual practice baseline (TBD) | −50 % vs manual |
| 3 | **Reviewer corrections** | edits per profile at review (flags, fact fixes, removals) | TBD | ↓ trend, all logged |
| 4 | **Shortlist relevance** | % of shortlisted candidates advanced to client interviews | practice baseline | ≥ practice baseline |
| 5 | **Freshness** | median age of cited sources | n/a | ≤ 90 days |
| 6 | **Review time** | human minutes per profile | TBD | ≤ 15 min |

## Protocol

- Every mandate run through the pipeline is audited on a fixed 50-item sample.
- Two reviewers independently; disagreements resolved by the partner, logged.
- Results (including failures) will be published in this repository as
  `results/` reports — methodology above, no cherry-picking.
- The **synthetic concept demo** (demo.matteiic.com) makes no performance claims
  and is excluded from all metrics.

## Fairness & safety checks

- Evidence samples screened for proxy-discrimination signals (age, origin,
  gender-coded language) before shortlist assembly.
- Any flag of systematic bias pauses the pipeline for human review — by design,
  not as an exception.
