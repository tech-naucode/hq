# Quality Gates Registry

Every operating company in NAUCode runs work through these gates. AI workers
do 80% of the work; human operators sign at 20% of the points. This document
defines exactly where humans must show up.

Inspired by AINS OPC pattern (kế thừa từ vibe-opc-orchestrator) — adapted for
NAUCode 2-desk model.

## Gate registry

### G-01 · Proposal to enterprise

**Trigger:** Any proposal artifact in `engagement-*/processing/human-review/proposal-*.md`
or `sales-pipeline/deals/proposal-out/*`
**Owner:** Principal (deal value ≥ AUD 20,000) / Managing (< AUD 20,000)
**SLA:** 24h from artifact ready
**Required action:** Read + edit + APPROVED FOR SEND comment + signature
**AI cannot bypass:** `proposal-publisher` agent in `sales-pipeline` refuses
send without `APPROVED FOR SEND` from owner role.

### G-02 · Deliverable to client

**Trigger:** Any artifact in `engagement-*/output/`
**Owner:** Managing
**SLA:** Per engagement SLA (typically 48h before client deadline)
**Required action:** Spot-check 1 in 3 minimum, full review for first 3
engagements with each new fellow team.
**AI cannot bypass:** `engagement-publisher` agent refuses send without
Managing signature.

### G-03 · Contract / SOW signing

**Trigger:** Any artifact in `compliance/contracts/processing/human-review/`
or sub-equivalent in engagement repos
**Owner:** Both — Managing drafts, Principal countersigns
**SLA:** Within 5 business days of negotiation close
**Required action:** Legal review (external counsel if first time per contract
type), then both signatures.

### G-04 · Vendor PO / Payment

**Trigger:** Any payment request in `vendor-*/processing/payment/`
**Owner:** Managing (< AUD 5,000) / Both (AUD 5,000 — 20,000) / Principal
countersign (> AUD 20,000)
**SLA:** 48h
**Required action:** Verify deliverable received against PO terms; confirm
non-circumvention clause holding.

### G-05 · IP release / Methodology version

**Trigger:** Any artifact moving from `lift/versions/draft/` to
`lift/versions/internal-use/`, `client-licensed/`, or `public-release/`
**Owner:** Principal
**SLA:** 1 week (this is not urgent)
**Required action:** Confirm:
- DSR audit passing on the version
- License model defined (if licensed)
- Backward compatibility note for existing licensees

### G-06 · Thought leadership publish

**Trigger:** Any artifact in `mkt-branch/output/processing/publish-ready/`
**Owner:** Principal (voice/positioning) + Managing (publish window check)
**SLA:** 48h
**Required action:** Brand-guardian skill must report PASS first. Principal
reads for strategic alignment. Managing confirms publish window and channel
rules per `mkt-branch/agents/publisher/AGENTS.md`.

### G-07 · Monthly review

**Trigger:** First Monday of each month
**Owner:** Both
**SLA:** Same week
**Required action:**
- Review `knowledge/03-ai-ready/monthly-review-*.md` (HR AI compiles)
- P&L per operating company
- Quality scorecard per AI worker
- Update routing-rules.md and quality-gates.md if patterns emerged
- Decide on add/remove of operating companies for next month

## Gate metadata schema

When operating companies log a gate event, they use this format in their
respective `quality-events.jsonl`:

```json
{
  "gate": "G-01",
  "timestamp": "2026-05-11T14:23:00Z",
  "company": "engagement-techcorp-2026q3",
  "artifact_path": "processing/human-review/proposal-v3.md",
  "owner_required": "principal-consultant",
  "owner_acted": "principal-consultant",
  "decision": "approved",
  "comment_link": "https://github.com/.../issues/12#comment-345"
}
```

## Anti-patterns

- ❌ AI worker waiting > SLA without escalating → must escalate to HQ at SLA + 1h
- ❌ Human approving without reading → use AI to summarize, but signature
  requires reading the actual artifact
- ❌ Both humans approving routine ops gates → wastes capacity, violates
  no-overlap rule in `human-operators.md`
- ❌ Skipping G-02 for "quick wins" → quality leak. Spot-check minimum required.
- ❌ Adding gates without removing — gate count should stay 7-9, not creep to 15.

## Gate health monitoring

A weekly snapshot of gate metrics is auto-compiled by `hq/agents/` (when
those exist) and posted to `knowledge/02-structured/gate-health-*.md`.

Key metrics:

- Gate cycle time (artifact ready → human signed)
- SLA violations per gate per week
- Bypass attempts (AI tried to send without gate — should always be 0)
- Reviewer fatigue signal (rapid-fire approvals < 30 sec average per gate)

## TODO

- [ ] Define exact dollar thresholds in local currency (AUD vs USD vs VND)
- [ ] Wire `quality-events.jsonl` logging into Paperclip workflow
- [ ] First-time use of each gate: Principal walks Managing through the rationale
