---
title: Multi-Model Write Access Governance
type: decision
permalink: decisions/multi-model-write-access-governance
status: canonical
temporal_type: dynamic
valid_from: 2025-12-04
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-12-04
tags:
- decision
- governance
- multi-model
- security
- architecture
- grok
- canonical
---

# Multi-Model Write Access Governance

## Summary

This document establishes mandatory requirements for granting write access to the Basic Memory knowledge base for AI models beyond Claude. **No model receives write access until all readiness gates are passed.**

## Decision Date
2025-12-04

## Status
**FROZEN** — Proposal under development. No write access granted to non-Claude models.

## Participants
- Ed O'Connell (Human Orchestrator / Product Manager)
- Grok (VP Engineering role - proposal advocate)
- ChatGPT (CIO role - governance gatekeeper)
- Claude Opus 4.5 (Developer role - implementation assessment)

---

## Context

### The Proposal
Grant Grok symmetric read/write access to Basic Memory via MCP, enabling multi-model collaboration with ensemble effects.

### The Verdict
The proposal demonstrates technical feasibility but fails the bar for write-plane governance. Too many safeguards rely on:
- Ad-hoc Git (no runtime guardrails)
- Informal intuition ("we'll detect problems")
- Deferred implementation ("we'll add guardrails later")
- Directory-level pseudo-namespaces (no real ACLs)
- No TLS on MCP transport
- No test harness
- No cascade analysis

**Conclusion:** The epistemic core is sacred ground. Multi-model write access requires rigorous governance infrastructure before implementation.

---

## Mandatory Readiness Gates

No negotiation. No acceleration. No shortcuts.

### Gate 1: Proposal Freeze ✅
**Status:** ACTIVE

No write access for any non-Claude model until all subsequent gates are passed. We proceed methodically.

### Gate 2: Governance Roles
**Status:** NOT STARTED

Define and document:

| Role | Responsibility | Current Holder |
|------|---------------|----------------|
| Basic Memory Owner | Final authority on memory contents and structure | Ed O'Connell |
| Model Access Administrator | Grants/revokes model access, manages tokens | Ed O'Connell |
| Memory Integrity Officer | Monitors for corruption, enforces protocols | Ed O'Connell |

Even if all three roles are held by one person, the roles must exist and be documented.

**Relation to Lanesborough Protocol:** These roles extend the Human Orchestrator concept to infrastructure governance.

### Gate 3: Real Namespaces
**Status:** NOT STARTED

Implement:
- [ ] Read/write ACLs at MCP layer
- [ ] Per-model root directories (`/models/grok/`, `/models/gemini/`)
- [ ] Separately versioned Git trees (or branches) per model
- [ ] Per-model delta budgets (max writes/day, max bytes/write)
- [ ] Per-model input sanitizers

**Critical rule:** No model touches `/shared/` until merge-agent signoff.

### Gate 4: Merge Agent
**Status:** NOT STARTED

Build a mediation layer that:
- [ ] Intercepts all write requests
- [ ] Validates schema/format/taxonomy compliance
- [ ] Blocks suspicious deltas (size, frequency, content patterns)
- [ ] Enforces per-model write budgets
- [ ] Logs every action with full context
- [ ] Supports dry-run mode for testing

**Estimated scope:** ~200 lines of code (not 20).

**Prior art:** Ghost Writer's HANDOFF_ARTIFACTS.md pattern for inter-agent communication logging.

### Gate 5: TLS
**Status:** BLOCKED (awaiting Dan G consultation)

No further infrastructure work until MCP uses TLS. Non-negotiable.

**Current state:** 
- Caddy is installed on adambalm but disabled
- Caddy has `tls internal` capability for Tailscale domains
- Basic Memory HTTP runs on port 8765 (unencrypted)

**Path forward:**
- Consult Dan G about Caddy reactivation
- Configure Caddy as reverse proxy to port 8765
- Use `tls internal` (no external CA complexity)

**What NOT to do:** 
- No custom root CAs
- No iOS mobileconfig certificates
- No remote browser automation scenarios
- (See [[Ghost Writer - Project Documentation]] for lessons learned)

### Gate 6: Test Harness
**Status:** NOT STARTED

Must include:
- [ ] Destructive-write simulations
- [ ] Adversarial prompt injection attempts
- [ ] Ambiguity stress tests
- [ ] Conflict scenario simulations
- [ ] Recursive summarization traps
- [ ] Path traversal attempts
- [ ] Performance under rapid-fire writes

**Grok does not touch production until it passes all tests.**

**Prior art:** Ghost Writer achieved 137 tests, 68% coverage. Similar rigor required here.

### Gate 7: Periodic Checkpointing
**Status:** NOT STARTED

Implement automatic backups:
- [ ] Daily full snapshots
- [ ] Hourly diff snapshots
- [ ] Per-model session checkpoints
- [ ] Retention policy (30 days minimum)

### Gate 8: Eviction Switch
**Status:** NOT STARTED

Create a real command, not a config edit:

```bash
memoryctl terminate-model grok --immediate
```

This must:
- [ ] Kill active request chains
- [ ] Revoke model's access token
- [ ] Freeze merge-agent processing for that model
- [ ] Log the eviction event
- [ ] Notify the Memory Owner

### Gate 9: Threat Model
**Status:** NOT STARTED

Document attack vectors and mitigations for:
- [ ] Cascade corruption (one bad write propagates)
- [ ] Model-model feedback loops (echo chambers)
- [ ] Hallucinated schema rewrites
- [ ] Directory flooding (denial of service)
- [ ] Token leakage
- [ ] Conflict storms (rapid contradictory writes)
- [ ] Hallucinated MCP endpoints
- [ ] Operator error

### Gate 10: Phased Rollout
**Status:** NOT STARTED (requires Gates 1-9)

Only after all previous gates pass:

| Phase | Access Level | Duration | Exit Criteria |
|-------|-------------|----------|---------------|
| 1 | Read-only | 7 days | No errors, useful queries |
| 2 | Write proposals (no merge) | 14 days | Proposals pass validation |
| 3 | Merge-agent mediated writes | 14 days | No blocked writes, clean logs |
| 4 | Limited write scope | 30 days | Stable operation |
| 5 | Full symmetric `/shared/` access | Ongoing | 30 days stable logs |

---

## Implementation Estimates

Based on developer assessment:

| Phase | Work | Estimate |
|-------|------|----------|
| Phase 0: Infrastructure Hardening | TLS, attribution, logging, backups, rollback | 1-2 days |
| Phase 1: Governance Framework | Namespaces, proposals, merge agent, budgets, eviction | 3-5 days |
| Phase 2: Testing Infrastructure | Harness, adversarial tests, conflict sims, baselines | 2-3 days |
| Phase 3: Documentation | Threat model, runbooks, architecture updates | 1-2 days |
| **Total** | | **7-12 days** |

This does not include the phased rollout observation periods.

---

## Design Principles

### From Black Flag Protocol
- State confidence levels on all claims
- Distinguish provable from inferred
- Surface contradictions for human adjudication
- Never fabricate data or sources

### From Lanesborough Protocol  
- Human Orchestrator makes final decisions
- Visible debate between agents
- Document-based handoffs with explicit state
- Challenge proposals before accepting

### From Ghost Writer (Prior Art)
- Evidence tagging: `[verified]` vs `[inference]`
- Professional communication: no premature claims of success
- Commit discipline: RISK/ROLLBACK/EVIDENCE required
- Per-agent documentation for context preservation

---

## What This Enables (Future State)

Once all gates are passed:
- [capability] Multi-model memory access with isolation guarantees
- [capability] Ensemble effects from diverse model perspectives
- [capability] Auditable decision provenance across models
- [capability] Graceful degradation if any model misbehaves
- [capability] Human-controlled rollback at any point

---

## Current Blockers

| Blocker | Owner | Status |
|---------|-------|--------|
| TLS configuration | Dan G consultation | Pending |
| Governance roles documentation | Ed | Not started |
| Merge agent design | Ed + Claude | Not started |

---

## Relations

- extends [[Architecture Decision - Centralized Memory on adambalm]]
- implements [[Lanesborough Protocol]] (role definitions)
- implements [[Black Flag Protocol]] (epistemic hygiene)
- informed_by [[Ghost Writer - Project Documentation]] (prior patterns)
- referenced_in [[BOOTSTRAP]] (pending addition)
- part_of [[Memory System Backlog]]

---

## Changelog

| Date | Change | Author |
|------|--------|--------|
| 2025-12-04 | Initial governance framework | Claude Opus 4.5 |
