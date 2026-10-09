# Talent Radar — planned architecture

**Version:** 0.9 (public) · **Status: v0 concept · synthetic demo · prototype in
development.** Nothing here is deployed yet; this document is the plan the
prototype will be built against — and judged by.

## Pipeline (planned)

```
[mandate criteria]                       (human, structured form)
        │
        ▼
┌───────────────────────────────────────────────────┐
│ Source gathering — Claude API agents              │
│  • allow-listed public/permitted sources only     │
│  • every fact stored WITH its source + timestamp  │
└───────────────┬───────────────────────────────────┘
                ▼
┌───────────────────────────────────────────────────┐
│ Profile synthesis — Claude API                    │
│  • structured extraction → evidence objects       │
│  • role-comparison with reasoning, per criterion  │
│  • draft report assembly                          │
└───────────────┬───────────────────────────────────┘
                ▼
┌───────────────────────────────────────────────────┐
│ Human review layer                                │
│  • evidence-by-evidence verification UI           │
│  • flags require resolution; overrides logged     │
│  • partner sign-off → append-only signed shortlist│
└───────────────────────────────────────────────────┘
```

**Provenance mechanism:** source-grounded extraction via the **Anthropic Citations
API** (plus Claude's web-search tool for allow-listed discovery). The Citations API
guarantees valid citation pointers to supplied passages — it does not guarantee the
truth of the underlying source, correct identity matching or complete coverage.
Application-level checks and human review still assess support, identity, completeness
and conflicts; implementation must account for the documented interplay between
citations and strict structured outputs (parsing and validation are specified separately).

## v0 scope — in / out (deliberate cuts)

| In (v0 prototype) | Out (later, or manual) |
|---|---|
| One mandate type: VP/Director engineering roles | Other function families |
| 3–5 allow-listed public source types | Open-ended source discovery |
| One Claude call per source, citations stored | Agent swarms / multi-step planning |
| Evidence table + per-criterion comparison | Dedup engine |
| Review UI + append-only signed shortlist | Conflict auto-detection (manual for now) |
| Evaluation harness (see EVALUATION.md) | Freshness scoring (source dates, manual triage) |
| PII scrub step before every inference | SSO / multi-tenant hardening |

The three deferred items above are each a sub-project; pretending otherwise in a
v0 plan is how one-person roadmaps die.

## Stack (planned — one backend, one runtime)

| Layer | Choice | Why |
|---|---|---|
| Inference | **Claude API (Anthropic), first-party, Citations** | source-grounding behaviour; credits via Claude Startups if accepted |
| App + API | **Next.js route handlers** (single deployable) | review UI and API in one runtime for a one-person team |
| Async jobs | managed queue (Inngest / pg-boss) | rate-limit discipline, retries — without a second service to operate |
| Storage | **Postgres + pgvector** (Neon/Supabase, Canadian region) | evidence objects + similarity for market mapping |
| Hosting | Canadian region at rest | Québec privacy principles (Law 25) |

**Cross-border reality, stated plainly:** data is hosted in Canada at rest, but
inference payloads (career information) are processed by Anthropic's API in the
US under Anthropic's Commercial Terms — including the no-training commitment.
The Law 25 cross-border transfer assessment is documented before any real
candidate data enters the pipeline.

## Signature mechanism

A signed shortlist is an **append-only record**: partner name + content hash +
timestamp. Re-signing appends a new record; nothing is mutated. The audit log is
the accountability surface clients (and regulators) can inspect.

## Design constraints (non-negotiable)

1. **Provenance or nothing** — a fact without a source cannot enter a profile.
2. **No public-model training** on career data, ever.
3. **Every shortlist is signed** by a named human; no automated hiring decisions.
4. **Physiological/coaching data (later module) lives in a separate system** and
   never feeds employment-assessment contexts.
5. Candidate data: minimum necessary, retention limits, deletion honoured.

## Sources policy (v0)

Allow-listed public and permitted sources only: company press releases and
engineering blogs, conference and meetup programs, public regulatory filings,
open-web publications. **No LinkedIn scraping; no ToS-violating collection** —
the legal minefield of the talent-intelligence category is not our growth
strategy. The v0 allow-list is published in the prototype repository.

## What we will NOT build

- Automated hiring decisions or unsupervised shortlists.
- Emotion inference or biometric scoring of candidates.
- Scraping of private/personal data.
