---
title: Naming and Structure Convention
type: note
permalink: protocols/naming-and-structure-convention
tags:
- protocol
- convention
- naming
- structure
- governance
status: canonical
temporal_type: static
valid_from: 2025-12-02
last_verified: 2025-12-02
---

# Naming and Structure Convention

**Purpose:** Establish consistent naming and organization rules for the Basic Memory knowledge base.

**Effective:** 2025-12-02
**Applies to:** All new files. Existing files grandfathered unless actively causing problems.

---

## Filename Rules

1. **Use kebab-case:** `black-flag-protocol.md` not `Black Flag Protocol.md`
2. **Descriptive names:** No date-only names, no cryptic abbreviations
3. **No type prefixes:** Folder provides type context
4. **Match permalink when possible:** Reduces cognitive overhead

---

## Folder Structure

| Folder | Purpose | Example |
|--------|---------|---------|
| `protocols/` | Governing protocols | `black-flag-protocol.md` |
| `decisions/` | Architecture Decision Records | `centralized-memory-adambalm.md` |
| `diagnostics/` | Troubleshooting reports, case studies | `sigint-bug-analysis.md` |
| `workspace/hardware/` | Machine specifications | `adambalm-server.md` |
| `workspace/specifications/` | Technical specifications | `cross-machine-context.md` |
| `workspace/planning/` | Vision, roadmaps, next steps | `context-system-vision.md` |
| `workspace/browser-sessions/` | Archived session snapshots | `chrome-2025-11-20.md` |
| `sca-projects/` | SCA work products | Subfolders as needed |
| `non-fiction/conversations/` | Essays, dialogues | `institutional-backpropagation.md` |
| `tests/` | Test documents | `ground-truth-test.md` |

---

## Root Directory

**Allowed in root:**
- `BOOTSTRAP.md` — AI initialization
- `README.md` — Repository overview
- `CLAUDE.md` — Repository conventions for Claude Code

**Not allowed in root:**
- Empty stub files
- Orphan documents that belong in a folder
- Date-only filenames

---

## Frontmatter Requirements

All documents MUST include:

```yaml
---
title: Human-Readable Title
type: note
permalink: folder/kebab-case-name
tags:
  - relevant
  - tags
status: canonical | draft | superseded | deprecated | archived
temporal_type: static | dynamic | point-in-time
valid_from: YYYY-MM-DD
last_verified: YYYY-MM-DD
---
```

**Optional fields:**
- `valid_until:` — When document expires
- `supersedes:` — What this replaces
- `superseded_by:` — What replaced this

---

## Grandfathering

Existing files with spaces in filenames (e.g., `Black Flag Protocol.md`) are acceptable. Do not rename unless:
- The filename actively causes a scripting/automation problem
- You're already editing the file for other reasons

New files MUST follow kebab-case.

---

## Enforcement

- **AI agents:** Follow this convention when creating files via `write_note`
- **Human review:** Monthly audit for orphan files and frontmatter gaps
- **Automated:** Future git hooks or CI could validate (not yet implemented)

---

## Relations

- extends [[BOOTSTRAP]]
- implements [[Black Flag Protocol]] (Clause 3: documentation standards)
- applies_to all folders in this knowledge base