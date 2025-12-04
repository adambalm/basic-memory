---
title: Frontmatter Governance and Enforcement
type: decision
permalink: decisions/frontmatter-governance-and-enforcement
status: draft
temporal_type: dynamic
valid_from: 2025-12-04
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-12-04
tags:
  - decision
  - frontmatter
  - governance
  - temporal-validity
  - tooling
---

# Frontmatter Governance and Enforcement

**Decision Status:** Draft — options identified, decision pending
**Owner:** Ed O'Connell
**Created:** 2025-12-04

---

## Context

On 2025-12-04, a systematic audit revealed that 33 of ~40 documents in the Basic Memory knowledge base had incomplete frontmatter. The Temporal Validity Protocol (established 2025-11-26) specifies required fields that the `write_note` tool cannot populate.

**Incident documented in:** [[Frontmatter Standardization Gap - Incident Report]]

### The Problem

The `write_note` MCP tool auto-generates frontmatter from its parameters:
- Accepts: `title`, `folder`, `tags`
- Hardcodes: `type: note`, `permalink`
- Cannot set: `status`, `temporal_type`, `valid_from`, `valid_until`, `supersedes`, `superseded_by`, `last_verified`

The Temporal Validity Protocol requires all of these fields. This creates a **protocol-capability gap**: governance rules that tooling cannot enforce.

### Constraints

1. Basic Memory is an external project — we cannot modify `write_note` behavior
2. Claude agents are stateless — they don't remember to follow multi-step procedures unless prompted
3. Multiple access patterns exist (Claude Code, Claude Desktop, potentially ChatGPT/Gemini)
4. Human review bandwidth is limited

---

## Options Under Consideration

### Option A: Two-Pass Creation Protocol

**Description:** Formalize the workaround used during remediation. Every document creation requires:
1. `write_note` to create document with content
2. `edit_note` to fix frontmatter immediately after

**Pros:**
- Works today, no tooling changes needed
- Agents can follow if instructed

**Cons:**
- Relies on agent compliance (no enforcement)
- Easy to forget step 2
- Verbose — doubles tool calls for every new document
- BOOTSTRAP.md would need to mandate this clearly

**Enforcement:** None — honor system

---

### Option B: Pre-Commit Hook Validation

**Description:** Git hook that validates frontmatter before allowing commits. Rejects commits with incomplete frontmatter.

**Pros:**
- Catches problems before they enter the repository
- Works regardless of how document was created
- Enforcement is automatic

**Cons:**
- Only catches issues at commit time, not creation time
- Requires implementation effort
- May block legitimate work if hook is too strict
- Doesn't help non-git workflows (if any)

**Enforcement:** Automatic at commit time

---

### Option C: Scheduled Audit Script

**Description:** Cron job that scans all documents periodically, reports incomplete frontmatter.

**Pros:**
- Catches drift over time
- Doesn't block workflows
- Can generate reports for human review

**Cons:**
- Detection is delayed (not prevention)
- Requires someone to act on reports
- Doesn't prevent the problem, only detects it

**Enforcement:** Periodic detection, manual remediation

---

### Option D: Accept as Technical Debt

**Description:** Acknowledge the gap, document it, rely on periodic manual audits.

**Pros:**
- No implementation effort
- Honest about current state

**Cons:**
- Problem will recur
- Governance claims become theater
- Temporal Validity Protocol promises more than it delivers

**Enforcement:** None

---

### Option E: Request Basic Memory Enhancement

**Description:** File issue/PR with Basic Memory project requesting additional frontmatter parameters.

**Pros:**
- Fixes root cause
- Benefits other users of Basic Memory

**Cons:**
- Dependent on external project timeline
- May not be accepted
- Doesn't help in the meantime

**Enforcement:** Depends on implementation

---

### Option F: Wrapper Tool

**Description:** Create a local wrapper script/function that calls `write_note` then `edit_note` with proper frontmatter.

**Pros:**
- Automates the two-pass pattern
- Single command for compliant document creation

**Cons:**
- Requires implementation
- Agents must know to use wrapper instead of raw `write_note`
- Adds complexity to tooling stack

**Enforcement:** None — must choose to use wrapper

---

## Decision Criteria

When evaluating options, consider:

1. **Prevention vs. Detection:** Does it stop bad documents or just find them later?
2. **Enforcement mechanism:** Honor system, automated check, or human review?
3. **Implementation effort:** Hours, days, or dependent on external projects?
4. **Agent compatibility:** Can Claude/ChatGPT/Gemini follow it reliably?
5. **Maintenance burden:** Ongoing cost to keep it working?

---

## Recommendation

*[To be completed after discussion with Ed]*

---

## Decision

*[To be completed when decision is made]*

---

## Consequences

*[To be completed when decision is made]*

---

## Related Documents

- [[Frontmatter Standardization Gap - Incident Report]] — Documents the incident
- [[Temporal Validity Protocol]] — Defines frontmatter requirements
- [[Naming and Structure Convention]] — Defines field list
- [[Memory System Backlog]] — Tracks implementation
- [[BOOTSTRAP]] — Would need update if Option A chosen
