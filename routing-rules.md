# Routing Rules — Incoming Task → Operating Company

When a new task / brief / signal arrives, this document tells every AI worker
which company repo should own it. The default routing rule lives at the top;
specific overrides follow.

## Default

If no rule below matches, route to **HQ** (this repo) and tag the issue with
`needs-routing-decision`. A human operator decides where it goes within 24h
and adds the new rule to this file.

## By task type

| Trigger keyword / signal | Route to | Owner role |
|---|---|---|
| `IP`, `patent`, `license`, `methodology brokering`, `trade secret`, `know-how transfer` | `ipcom` | Principal |
| `Australia`, `AU`, `Oceania`, `NZ`, `New Zealand`, `engineering certainty campaign` | `gtm-au` | Principal (deals) / Managing (campaign ops) |
| `consulting engagement`, `Propozel project`, `discovery sprint`, `LIFT solution pitch for client` | `consult` | Managing |
| `LIFT method`, `Certainty Units`, `DSR`, `methodology version`, `lift solution pitch (artifact-level)` | `lift` | Principal |
| `lead`, `inbound`, `RFP`, `proposal request`, `qualification` | `sales-pipeline` | Managing (qualify) / Principal (close) |
| `blog`, `content`, `thought leadership`, `social`, `case study`, `webinar` | `mkt-branch` | Principal (voice) / Managing (cadence) |
| `lesson`, `retrospective`, `post-mortem`, `pattern`, `playbook`, `framework draft` | `knowledge` | Both |
| `brand voice`, `lexicon update`, `do-not list`, `permitted-customers update`, `regulatory claim` | `brand` | Principal |
| `MSA`, `NDA`, `IP assignment`, `contract template`, `compliance calendar`, `data protection policy` | `compliance` | Managing (drafting) / Principal (sign) |

## By revenue impact

| Deal value | Route to | Approver |
|---|---|---|
| AUD < 5,000 | Direct to operating company (delivery / vendor PO) | Managing |
| AUD 5,000 — 20,000 | Operating company + Managing review | Managing |
| AUD 20,000 — 50,000 | Operating company + joint review | Both |
| AUD > 50,000 | `sales-pipeline` → joint review → Principal closes | Principal |
| Recurring AUD > 5,000 / month | Joint review for category creation | Both |

## By urgency

| Priority | Response SLA | Notify |
|---|---|---|
| P0 — system down, client escalation, security incident | 30 min | Both immediately |
| P1 — revenue at risk, deadline within 24h | 4h | Owner role |
| P2 — strategic decision needed | 24h | Owner role |
| P3 — operational, non-urgent | 72h | Owner role |
| P4 — research / exploration | weekly batch | None |

## Cross-company workflows (pre-defined chains)

These workflows touch multiple companies. Each step has a defined output that
triggers the next.

### Enterprise deal flow (new client)

```
inbound signal
  → sales-pipeline (qualify ICP, draft proposal)
  → joint review if AUD 20-50K, Principal if > 50K
  → consult (spawn engagement-<client>-<period> repo)
  → consult uses lift (apply methodology) + vendor-<fellow> (delivery capacity)
  → compliance (contract sign)
  → knowledge (capture lessons post-engagement)
```

### IP commercialization flow

```
methodology pattern signal (from consult engagement)
  → knowledge (codify pattern)
  → lift (if it fits LIFT framework) OR method-<new> (if standalone)
  → ipcom (assess commercial viability, define licensee profile)
  → compliance (license terms draft)
  → Principal sign
```

### Thought leadership flow

```
insight from engagement or methodology release
  → knowledge (raw note)
  → mkt-branch (draft content, run brand-guardian check)
  → brand (regulatory claims check, lexicon compliance)
  → Principal review
  → publish via mkt-branch publisher gate
```

## Update protocol

This file is updated by HQ humans (Principal or Managing). Operating companies
that find an unmatched task pattern raise it as an issue in this repo with
label `routing-rule-proposal`. HQ reviews weekly.

## TODO

- [ ] Validate routing keywords against Paperclip's actual task classification
- [ ] Add language-specific routing (Vietnamese inbound → which company defaults?)
- [ ] Define escalation when operating company refuses task ("not my scope")
