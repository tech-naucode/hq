---
schema: agentcompanies/v1
kind: company
slug: hq
name: NAUCode HQ
description: >
  Orchestration layer for Principal + Managing Consultant. Houses cross-cutting
  governance: routing rules, quality gate registry, IP portfolio map, and human
  operator scope. Does NOT execute operational work — that lives in ipcom,
  consult, gtm-au, lift, mkt-branch, sales-pipeline. HQ defines WHO decides WHAT.
version: 0.1.0
license: proprietary
tags:
  - hq
  - orchestration
  - governance
metadata:
  parent_org: NAUCode
  primary_language: en
  approval_required: true
  human_operators:
    - role: principal-consultant
      scope:
        - strategy
        - ip
        - key-account-c-level
        - deals-above-50k
        - methodology-licensing
    - role: managing-consultant
      scope:
        - delivery
        - vendor-mgmt
        - p-and-l
        - deals-below-20k
        - fellow-team-orchestration
  routes_to:
    - ipcom
    - gtm-au
    - consult
    - lift
    - mkt-branch
    - sales-pipeline
    - knowledge
    - brand
    - compliance
---

# NAUCode HQ

> **"HQ defines WHO decides WHAT. Operating companies decide HOW."**

This repo is the governance anchor for the NAUCode 2-desk + fellow + enterprise
operating model. It contains no operational SOPs and no agent workforce.
Everything here is a **decision-rule document** that operating companies read.

## What lives here

| File | Purpose |
|---|---|
| [`human-operators.md`](human-operators.md) | Principal + Managing scope, decision boundaries |
| [`routing-rules.md`](routing-rules.md) | Incoming task type → which company repo handles it |
| [`quality-gates.md`](quality-gates.md) | Gate registry (G-01..G-07) with owner + threshold |
| [`portfolio.md`](portfolio.md) | IP portfolio map + pointers to all operating units |

## What does NOT live here

- Operational SOPs (those live in each operating company)
- AI workforce / agents (those serve the operating companies)
- Deliverables, proposals, invoices (those live in `consult/engagement-*`, `compliance`)
- Brand voice, lexicon (lives in `brand/`)
- Lessons / Second Brain content (lives in `knowledge/`)

## How operating companies use HQ

Each operating company (`ipcom`, `consult`, `gtm-au`, etc.) reads HQ's documents
on every decision point:

- Before sending anything to a client → check `quality-gates.md`
- When unsure which company should pick up a task → check `routing-rules.md`
- When making a strategic decision → check `human-operators.md` for who owns it

## Status

| Section | Status |
|---|---|
| Human operator scope | DRAFT — names + boundaries need filling |
| Routing rules | DRAFT — covers core types, expand as new operating units come online |
| Quality gates | DRAFT — G-01..G-07 outlined, thresholds TBD per business reality |
| Portfolio | LIVE — reflects current 7 operating units + 3 shared infra |
