# Talent Radar — planned architecture

**Version:** 0.9 (public) · Status: design. Nothing here is deployed yet; this
document is the plan the prototype will be built against — and judged by.

## Pipeline (planned)

```
[mandate criteria]                       (human, structured form)
        │
        ▼
┌───────────────────────────────────────────────────┐
│ Source gathering — Claude API agents              │
│  • public/permitted sources only, allow-listed    │
│  • every fact stored WITH its source + timestamp  │
│  • dedupe, conflict detection, freshness scoring  │
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
│  • partner sign-off → immutable signed shortlist  │
└───────────────────────────────────────────────────┘
```

## Stack (planned)

| Layer | Choice | Why |
|---|---|---|
| Inference | **Claude API (Anthropic), first-party** | reasoning quality, source-grounding behaviour; credits via Claude Startups if accepted |
| Storage | PostgreSQL + pgvector | evidence objects + similarity for market mapping |
| Queue/agents | Python (FastAPI + background workers) | agent orchestration, retries, rate-limit discipline |
| App | Next.js (internal tool) | review UI, auth, audit log |
| Hosting | Canada-first cloud regions | Québec privacy principles (Law 25) from day one |

## Design constraints (non-negotiable)

1. **Provenance or nothing** — a fact without a source cannot enter a profile.
2. **No public-model training** on career data, ever.
3. **Every shortlist is signed** by a named human; the audit log is append-only.
4. **Physiological/coaching data (later module) lives in a separate system** and
   never feeds employment-assessment contexts.
5. Candidate data: minimum necessary, retention limits, deletion honoured.

## What we will NOT build

- Automated hiring decisions or unsupervised shortlists.
- Emotion inference or biometric scoring of candidates.
- Scraping of private/personal data; allow-listed public sources only.
