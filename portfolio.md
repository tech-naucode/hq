# NAUCode Portfolio Map

Current shape of NAUCode operating model. Updated as companies come online,
get deprecated, or shift role.

## Architecture diagram

```
         ┌──────────────────────────────────────────┐
         │      HUMAN OPERATORS (not in git)        │
         │   Principal Consultant + Managing        │
         └──────────────┬───────────────────────────┘
                        │
   ┌────────────────────┼───────────────────────────┐
   │                    │                            │
   ▼                    ▼                            ▼
 ┌───┐         ┌──────────────────┐         ┌──────────────┐
 │hq │ ←reads─ │ OPERATING ENGINES│         │   SHARED     │
 │   │         │                  │  ──→    │INFRASTRUCTURE│
 └───┘         │ ip-com            │         │              │
   ▲           │ gtm-au           │         │ knowledge    │
   │           │ consult          │         │ brand        │
   └───reads── │ lift             │ ←reads─ │ compliance   │
               │ mkt-branch        │         │              │
               │ sales-pipeline   │         └──────────────┘
               └──────────────────┘
                        │
                        │ spawns on demand
                        ▼
               ┌──────────────────┐
               │ SPAWN INSTANCES  │
               │                  │
               │ engagement-*     │
               │ vendor-*         │
               │ method-* (other  │
               │   than lift)     │
               └──────────────────┘
```

## Operating engines (long-lived, 1 per function)

| Repo | Function | Status | Owner role | Notes |
|---|---|---|---|---|
| [`ip-com`](https://github.com/tech-naucode/ip-com) | IP commercialization | Live | Principal | Identifies, evaluates, packages, brokers IP deals |
| [`gtm-au`](https://github.com/tech-naucode/gtm-au) | Oceania GTM | Live | Principal (deals) / Managing (campaign) | Operationalizes OPT Oceania launch playbook |
| [`consult`](https://github.com/tech-naucode/consult) | Consulting delivery | Live | Managing | Agent layer under Propozel platform |
| [`lift`](https://github.com/tech-naucode/lift) | LIFT methodology IP asset | Draft | Principal | Developed under DSR framework |
| [`mkt-branch`](https://github.com/tech-naucode/mkt-branch) | Marketing + thought leadership | Draft | Principal (voice) / Managing (cadence) | References `brand/` for kit |
| [`sales-pipeline`](https://github.com/tech-naucode/sales-pipeline) | Central deal pipeline | Draft | Both | Lead intake → proposal → close |

## Shared infrastructure (1 instance, used by all)

| Repo | Purpose | Status | Notes |
|---|---|---|---|
| [`knowledge`](https://github.com/tech-naucode/knowledge) | 3-tier Second Brain | Draft | Raw / structured / ai-ready |
| [`brand`](https://github.com/tech-naucode/brand) | Brand kit single source of truth | Draft | Voice, lexicon, do-not list, permitted customers, regulatory claims |
| [`compliance`](https://github.com/tech-naucode/compliance) | Contracts + compliance calendar | Draft | MSA, NDA, IP assignment templates |

## Infrastructure (not company-shaped)

| Repo | Purpose |
|---|---|
| [`n-clerk`](https://github.com/tech-naucode/n-clerk) | Paperclip deployment overlay (single-tenant) |

## Spawn instances (none yet)

Spawned on demand, 1 per real-world instance:

- `engagement-<client>-<period>` — per enterprise deal
- `vendor-<fellow-team>` — per fellow dev team relationship
- `method-<name>` — per methodology IP asset beyond LIFT (none planned)

Naming convention is enforced by routing-rules.md.

## External (not in tech-naucode org but referenced)

| External | Repo / URL | Referenced by |
|---|---|---|
| Propozel platform | https://propozel.com (`2ngnhan/propozel`) | `consult` (system-of-record), `lift` (operationalization) |
| LIFT UI prototype | `2ngnhan/lift-pitch` | `lift` (artifact builder UI) |
| DSR workshop content | `2ngnhan/may26ws` | `lift` (content source for method development) |
| Oceania launch playbook | `2ngnhan/naucode-opt-playbook` | `gtm-au` (source-of-truth playbook) |

These may be moved into `tech-naucode/` over time — separate reorganization
project tracked elsewhere.

## Deprecation candidates

None currently. When deprecating, an operating company is:
1. Archived (not deleted) — readonly state, content preserved
2. Removed from `routing-rules.md`
3. Listed here under a "Deprecated" section with rationale

## Update cadence

This file is reviewed at monthly G-07 review. Lightweight updates (one new
spawn instance, one description change) can happen any time via PR with both
operators as required reviewers.
