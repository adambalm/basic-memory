---
title: Frontmatter Standardization Gap - Incident Report
type: incident-report
permalink: diagnostics/frontmatter-standardization-gap-incident-report
status: canonical
temporal_type: point-in-time
valid_from: 2025-12-04
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-12-04
tags:
  - incident-report
  - frontmatter
  - temporal-validity
  - governance
  - tooling-gap
---

# Frontmatter Standardization Gap - Incident Report

**Incident Date:** 2025-12-04
**Reported By:** Claude Opus 4.5 (claude.ai)
**Scope:** Basic Memory knowledge base frontmatter compliance

---

## Summary

During routine document maintenance, discovered that 33 of approximately 40 documents in the Basic Memory knowledge base had incomplete frontmatter. Documents were missing fields required by the Temporal Validity Protocol: `status`, `temporal_type`, `valid_from`, `valid_until`, `supersedes`, `superseded_by`, and `last_verified`. Three documents also had malformed duplicate frontmatter blocks.

---

## Timeline

| Time | Event |
|------|-------|
| 2025-11-26 | Temporal Validity Protocol established, frontmatter requirements defined |
| 2025-11-26 to 2025-12-03 | Documents created via various methods with inconsistent frontmatter |
| 2025-12-04 ~15:00 | Duplicate frontmatter discovered in Multi-Model Write Access Governance |
| 2025-12-04 ~15:30 | Root cause identified: `write_note` tool limitation |
| 2025-12-04 ~16:00 | Systematic audit begun |
| 2025-12-04 ~17:00 | All 33 documents repaired via `edit_note` |

---

## Impact

**Documents Affected:** 33 of ~40 documents

**Breakdown:**
- 3 documents with duplicate frontmatter blocks (malformed YAML)
- 15 documents missing all temporal validity fields
- 15 documents missing some fields (typically `supersedes`, `superseded_by`, `valid_until`)

**Data Loss:** None. Content intact; only metadata incomplete.

**Operational Impact:** 
- Temporal Validity Protocol rules unenforceable (no metadata to check)
- Staleness detection impossible (no `last_verified` dates)
- Supersession chains broken (no `supersedes`/`superseded_by` links)

---

## Root Cause Analysis

### Proximate Cause

The `write_note` tool auto-generates minimal frontmatter from its parameters:
- `title` → title field
- `folder` → used in permalink
- `tags` → tags field
- Hardcoded: `type: note`

The tool has **no parameters** for: `status`, `temporal_type`, `valid_from`, `valid_until`, `supersedes`, `superseded_by`, `last_verified`.

### Contributing Factor: Duplicate Frontmatter

When agents included frontmatter in the `content` parameter (attempting to add missing fields), Basic Memory prepended its auto-generated block, resulting in two `---` blocks — invalid YAML.

### Systemic Cause

**Protocol-Capability Gap:** The Temporal Validity Protocol specifies frontmatter requirements that the primary document creation tool cannot fulfill. The protocol assumed capabilities that don't exist in the tooling.

### Why It Wasn't Caught Earlier

- No automated validation of frontmatter completeness
- No pre-commit hooks checking for required fields
- Manual review didn't occur until this session
- Obsidian displays frontmatter as "properties" regardless of completeness — visual inspection doesn't highlight gaps

---

## Remediation Performed

### Immediate Fix

Used `edit_note` with `find_replace` operation to:
1. Merge duplicate frontmatter blocks (3 documents)
2. Add missing fields to all 33 documents
3. Standardize field order across all documents
4. Update `type` field to be more specific than generic "note"

### Standard Field Order Established

```yaml
---
title: [Title]
type: [decision|diagnostic|specification|documentation|protocol|etc.]
permalink: [folder/kebab-case-name]
status: [canonical|draft|archived|resolved|completed]
temporal_type: [static|dynamic|point-in-time]
valid_from: [YYYY-MM-DD]
valid_until: [null or YYYY-MM-DD]
supersedes: [null or link]
superseded_by: [null or link]
last_verified: [YYYY-MM-DD]
tags:
  - [tag1]
  - [tag2]
---
```

---

## Prevention

**Status:** Decision pending

The immediate symptom is addressed, but the systemic gap remains:
- `write_note` still cannot populate temporal validity fields
- No automated enforcement exists
- Future documents created via `write_note` will have the same problem

**Options under consideration:**
- Pre-commit hooks validating frontmatter
- Wrapper script/protocol for `write_note` + `edit_note` sequence
- Update Temporal Validity Protocol to acknowledge limitation
- Accept as ongoing manual maintenance burden
- Request Basic Memory tool enhancement

**Decision tracked in:** [[Frontmatter Governance and Enforcement]]

---

## Lessons Learned

1. **Protocols must align with tool capabilities.** The Temporal Validity Protocol specified requirements without verifying the tools could meet them.

2. **Governance-by-documentation has limits.** Without enforcement mechanisms, compliance depends entirely on agent discipline and human review.

3. **Visual tools can mask problems.** Obsidian's properties panel displays whatever frontmatter exists without indicating what's missing.

4. **Two-pass creation may be necessary.** Until tooling improves, `write_note` followed by `edit_note` may be the required pattern.

---

## Related Documents

- [[Temporal Validity Protocol]] — Defines frontmatter requirements
- [[Naming and Structure Convention]] — Defines frontmatter field list
- [[Frontmatter Governance and Enforcement]] — Pending decision on prevention
- [[Memory System Backlog]] — Tracks implementation work

---

## Document Metadata Note

This document was created using the two-pass method: `write_note` for content, then `edit_note` to complete frontmatter — the same workaround this incident report documents.
