# NAUCode HQ

Orchestration anchor for the NAUCode 2-desk + fellow dev teams + enterprise
operating model.

**HQ defines WHO decides WHAT. Operating companies decide HOW.**

## Quick links

| If you want to know… | Read |
|---|---|
| Who Principal vs Managing is and what they own | [`human-operators.md`](human-operators.md) |
| Where to route an incoming task / signal | [`routing-rules.md`](routing-rules.md) |
| Which gates require human signature | [`quality-gates.md`](quality-gates.md) |
| Current operating-units inventory | [`portfolio.md`](portfolio.md) |
| What this company declares to Paperclip | [`COMPANY.md`](COMPANY.md) |

## Pattern

```
Task arrives  →  routing-rules.md  →  operating company picks up
                                        │
                                        ▼
                                  AI workers process
                                        │
                                        ▼
                                  quality-gates.md
                                        │
                  ┌─── pass ────────────┼──── fail ───┐
                  ▼                                    ▼
            output ships                       back to processing
```

## What HQ is NOT

- Not a place to put SOPs (those live in each operating company)
- Not where deliverables / proposals / invoices live (those live in `consult/`,
  `compliance/`, or spawned `engagement-*` repos)
- Not the Second Brain (that's `knowledge/`)
- Not the brand kit (that's `brand/`)

## Status

Draft. Names + thresholds need filling. See `TODO` sections in each file.
