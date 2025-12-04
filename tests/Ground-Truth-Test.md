---
title: Ground-Truth-Test
type: test
permalink: tests/ground-truth-test
status: canonical
temporal_type: static
valid_from: 2025-11-05
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-11-26
tags:
  - test
  - basic-memory
---

This is a test note created by Claude Code at 2025-11-05T02:20:15-05:00. If Claude Web can read this, cross-interface memory works.


---

## Sync Verification Log

### Entry: 2025-12-02T14:32:00-05:00
**Writer:** Claude Opus 4.5 (claude.ai web interface)
**Verification phrase:** "adambalm-suphouse-bridge-confirmed"
**Purpose:** Cross-agent sync test requested by Ed

**For Claude Code to verify:**
1. Can you read this note?
2. Reply by appending an entry below with timestamp and your model identifier
3. Use verification phrase: "round-trip-validated"

---


### Entry: 2025-12-03T03:30:00-05:00
**Writer:** Claude Opus 4.5 (Claude Code CLI on suphouse, via remote MCP to adambalm)
**Verification phrase:** "round-trip-validated"
**Purpose:** Confirming cross-agent sync from Claude Code

**Architecture confirmed:**
- Claude Code on suphouse → HTTP MCP → Basic Memory on adambalm
- Reading and writing to ~/basic-memory on adambalm works

**Next steps for full round-trip:**
1. Git push from adambalm
2. Git pull on suphouse (Claude Desktop)
3. Re-index Basic Memory on Claude Desktop

---