---
title: Temporal Validity Protocol
type: note
permalink: protocols/temporal-validity-protocol
tags:
  - protocol
  - versioning
  - temporal-validity
  - knowledge-management
  - multi-agent
status: canonical
temporal_type: static
valid_from: 2024-11-26
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-11-26
---

# Temporal Validity Protocol

An extension to the [[Black Flag Protocol]] for managing document validity, supersession, and temporal state in multi-agent knowledge systems.

## Purpose

As knowledge evolves, earlier decisions become outdated. Without explicit validity tracking, LLMs may cite stale information or contradict current architecture. This protocol establishes:

1. How documents declare their validity state
2. How LLMs should interpret and prioritize documents
3. How supersession chains are maintained
4. When human intervention is required

## Reference Implementation

Inspired by OpenAI's Temporal Agents pattern (June 2025), adapted for markdown-based knowledge bases with multi-agent access.

## Document Classification

### Temporal Types

Every decision or specification document has a temporal type:

| Type | Definition | Example |
|------|------------|---------|
| `static` | True from a point in time, never changes | "We chose Wagtail CMS on 2024-03-15" |
| `dynamic` | Currently true but may change | "Memory is centralized on adambalm" |
| `atemporal` | Always true regardless of time | "SQLite databases are machine-local" |

### Document Status

| Status | Meaning | LLM Behavior |
|--------|---------|--------------|
| `canonical` | Current authoritative version | **Cite freely** |
| `superseded` | Replaced by newer document | **Do not cite as current truth** |
| `draft` | Under development | Cite only if explicitly discussing drafts |
| `deprecated` | Discouraged but not replaced | Cite with caveat |
| `archived` | Historical record only | Never cite as guidance |

## Frontmatter Specification

All protocol and decision documents MUST include validity frontmatter:

```yaml
---
title: Document Title
status: canonical | superseded | draft | deprecated | archived
temporal_type: static | dynamic | atemporal
valid_from: YYYY-MM-DD
valid_until: null | YYYY-MM-DD
supersedes: null | [[Previous Document]]
superseded_by: null | [[Newer Document]]
last_verified: YYYY-MM-DD
---
```

### Field Definitions

- **status**: Current validity state (REQUIRED)
- **temporal_type**: How this truth behaves over time (REQUIRED for decisions)
- **valid_from**: Date this became true (REQUIRED)
- **valid_until**: Date this stopped being true (null if still valid)
- **supersedes**: Link to document(s) this replaces
- **superseded_by**: Link to document that replaced this (set when superseded)
- **last_verified**: Date a human confirmed this is still accurate

## LLM Bootstrap Rules

These rules MUST be included in any bootstrap/system prompt for agents accessing Basic Memory:

### Rule 1: Status Check
Before citing any decision or protocol document, check its `status` field:
- `canonical` → Safe to cite as current truth
- `superseded` → Follow `superseded_by` link, cite that instead
- `draft` → Only mention if user asks about work-in-progress
- `deprecated` → Mention with explicit caveat
- `archived` → Do not cite as guidance

### Rule 2: Supersession Chain
If a document is `superseded`, trace the chain:
```
Old Decision (superseded) 
  → superseded_by → Intermediate (superseded)
    → superseded_by → Current (canonical)
```
Always cite the terminal `canonical` document.

### Rule 3: Staleness Detection
If `last_verified` is older than 90 days AND `temporal_type` is `dynamic`:
- Flag to human: "This decision may be stale"
- Do not treat as authoritative without verification

### Rule 4: Conflict Resolution
If two `canonical` documents contradict:
1. Prefer the one with more recent `valid_from`
2. Flag the conflict to human
3. Do not synthesize or guess resolution

## Supersession Workflow

### When Architecture Changes

1. **Human creates new decision document** with:
   - `status: canonical`
   - `supersedes: [[Old Decision]]`
   - `valid_from: today`

2. **Human updates old document** frontmatter:
   - `status: superseded`
   - `superseded_by: [[New Decision]]`
   - `valid_until: today`

3. **Git commit** captures both changes atomically

### LLM-Assisted Supersession (Future)

When implemented, LLMs may:
- Detect potential staleness via semantic similarity
- Propose supersession (human approves)
- Draft new canonical document (human reviews)

LLMs MUST NOT unilaterally change document status.

## Verification Cadence

| Document Type | Verification Frequency |
|---------------|----------------------|
| Architecture decisions | Quarterly |
| Protocol definitions | Monthly |
| Tool configurations | Weekly |
| Contact/reference info | As-needed |

## Integration with Black Flag Protocol

This protocol extends Black Flag by adding:

- **Clause 15**: Validity Check
  > Before citing stored knowledge, verify document status is `canonical`. Superseded documents are historical record only.

- **Clause 16**: Staleness Flag
  > Dynamic decisions not verified within 90 days require human confirmation before treating as authoritative.

- **Clause 17**: Conflict Escalation
  > Contradictions between canonical documents MUST be flagged to human. Do not resolve by inference.

## Example: Marking a Decision Superseded

Before (old document):
```yaml
---
title: Architecture Decision - Distributed Sync
status: canonical
temporal_type: dynamic
valid_from: 2024-10-15
supersedes: null
superseded_by: null
---
```

After supersession:
```yaml
---
title: Architecture Decision - Distributed Sync
status: superseded
temporal_type: dynamic
valid_from: 2024-10-15
valid_until: 2024-11-26
supersedes: null
superseded_by: [[Architecture Decision - Centralized Memory on adambalm]]
---
```

## Implementation Status

- [x] Protocol specification (this document)
- [ ] Frontmatter added to existing decisions
- [ ] Bootstrap document created with LLM rules
- [ ] Black Flag Protocol updated with clauses 15-17
- [ ] Verification schedule established

## Relations

- extends [[Black Flag Protocol]]
- enables [[Lanesborough Protocol]] multi-agent consistency
- references OpenAI Temporal Agents pattern
- applies_to [[Architecture Decision - Centralized Memory on adambalm]]
