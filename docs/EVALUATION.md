# Talent Radar — evaluation plan

**Version:** 0.9 (public). We publish metrics only when measured; until then,
this page is the protocol definition — not the result.

## Baseline commitment (before the prototype runs)

The manual baseline is not "TBD" — it is a scheduled measurement: the next
**three parent-firm mandates** are tracked end-to-end (hours spent, sources
consulted, corrections during client review) and published in this repository
as `results/baseline-001` **before** the first prototype-assisted mandate runs.
Every "vs manual" claim below refers to that published baseline.

## Metrics

| # | Metric | Definition | Baseline | Target (prototype) |
|---|---|---|---|---|
| 1 | **Source accuracy** | % of audited evidence items whose claim matches its cited source | measured via baseline-001 | ≥ 95 % |
| 2 | **Research time** | wall-clock from mandate brief to review-ready profiles | measured via baseline-001 | −50 % or better vs published baseline |
| 3 | **Reviewer corrections** | edits per profile at review (fact fixes, removals) | measured via baseline-001 | ↓ trend, all logged |
| 4 | **Shortlist relevance** | % of shortlisted candidates advanced to client interviews | retrospective audit of the parent firm's last 10 mandates (instrument: mandate debrief files, coded to the same definition) | ≥ audited baseline |
| 5 | **Source freshness** | median age of cited sources | n/a | ≤ 90 days |
| 6 | **Review time** | human minutes per profile | measured via baseline-001 | ≤ 15 min |
| 7 | **Inter-reviewer agreement** | % of audit items where two reviewers agree | n/a | reported from the first batch |
| 8 | **API cost per mandate** | Claude API spend per completed research batch | n/a | reported with every results report |

Metric 7 costs nothing (two reviewers are already part of the protocol) and
metric 8 is the number a Claude Startups reviewer should expect us to track.

## Protocol

- Sampling: **25 stratified evidence items per research batch** (not 50 — the
  per-batch scope is smaller; strata: source type × criterion).
- Two reviewers independently; disagreements resolved by the partner; agreement
  rate reported with every batch.
- Results — **including failures** — are published in this repository under
  `results/`, methodology fixed above, no cherry-picking.
- The **synthetic concept demo** (demo.matteiic.com) makes no performance claims
  and is excluded from all metrics.

## Fairness & safety checks

- v0 instrument: a maintained lexicon of proxy-discrimination marker terms
  (age-coded, origin-coded, gender-coded phrasing) applied to every profile
  before shortlist assembly, plus a human check of all flags; a statistical
  eval set is a later milestone, and we say so rather than imply otherwise.
- Any confirmed bias signal pauses the pipeline for partner review — by design.
