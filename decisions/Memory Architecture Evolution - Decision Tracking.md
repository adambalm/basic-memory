---
title: Memory Architecture Evolution - Decision Tracking
type: note
permalink: decisions/memory-architecture-evolution-decision-tracking
tags:
- architecture
- evolution
- decision-tracking
- failure-modes
status: canonical
temporal_type: dynamic
valid_from: 2025-12-02
valid_until: null
last_verified: 2025-12-02
---

# Memory Architecture Evolution - Decision Tracking

**Document Type:** Living decision log
**Created:** 2025-12-02
**Purpose:** Track architectural evolution, identified failure modes, and open decision points

---

## Current Understanding (2025-12-02)

### Two Access Patterns Required

**Pattern A: Local Claude Code (on any machine)**
- Uses local stdio MCP server
- Reads/writes local files
- Works offline
- Syncs via git push/pull

**Pattern B: Remote clients (Gemini, ChatGPT, Claude Desktop on other machines)**
- Uses HTTP API on adambalm
- Requires network connectivity
- adambalm is their only access point

**adambalm is "canonical" because:**
1. Tiebreaker when conflicts arise
2. Only endpoint for Pattern B clients
3. NOT the only place writes can happen

---

## Identified Failure Modes

### FM1: Offline write conflicts with remote write

- suphouse offline, writes decisions/use-wagtail.md (canonical)
- adambalm writes decisions/use-wordpress.md (canonical)
- Git sync: both exist, both canonical, contradict
- **Gap:** No automated contradiction detection

### FM2: Supersession chain breaks offline

- v1 exists (canonical)
- adambalm creates v2 (supersedes v1)
- suphouse offline creates v3 (supersedes v1, doesn't know v2 exists)
- Post-sync: v3 supersession target wrong
- **Gap:** No chain integrity validator

### FM3: last_verified conflicts

- Same doc verified on two machines same day
- Git merge conflict on metadata
- **Mitigation:** Add last_verified_by field with machine name

### FM4: Stale index after git pull

- Pull brings new files
- Re-indexing takes time
- Queries during re-index return incomplete results
- **Gap:** No sync-in-progress indicator

### FM5: SIGINT bug blocks suphouse MCP

**Evidence from Claude Code logs:**
```
01:16:10.502Z Successfully connected to stdio server in 4090ms
01:16:10.503Z Connection established with capabilities
01:16:10.504Z Sending SIGINT to MCP server process
01:16:10.564Z MCP server process exited cleanly
```
- Claude Code kills server 1ms after successful connection
- **Status:** Immediate blocker on suphouse

### FM6: Claude Desktop routing unknown

- Where does this conversation's MCP route?
- Local stdio? Remote HTTP?
- Affects conflict prediction

### FM7: Simultaneous Claude instances

- Claude Code on suphouse + Claude Code on adambalm
- Both can write, no coordination
- **Gap:** No locking (probably acceptable for single user)

---

## What Needs To Exist

| Component | Purpose | Status |
|-----------|---------|--------|
| Local MCP on suphouse | Offline writes | BROKEN |
| HTTP server on adambalm | Remote clients | NOT RUNNING |
| Contradiction scanner | Detect FM1/FM2 | NOT IMPLEMENTED |
| Chain validator | Detect FM2 | NOT IMPLEMENTED |
| Sync indicator | Avoid FM4 | NOT EXPOSED |
| Reconciliation protocol | Conflict resolution | NOT SPECIFIED |

---

## Open Decision Points

### DP1: Fix SIGINT vs HTTP workaround?

- A: Debug Claude Code SIGINT behavior
- B: Use mcp-proxy to HTTP (bypass stdio)
- C: Both

### DP2: Every machine needs local MCP?

- Intended: Yes, for offline capability
- Needs confirmation

### DP3: Automated contradiction detection?

- Post-git-pull scan for conflicts?
- Engineering effort vs manual vigilance

### DP4: Reconciliation protocol details?

- How is human notified?
- What format for conflict report?
- What if human doesn't respond?

### DP5: Claude Desktop routing?

- Need to determine actual path
- Test: where does this write appear first?

---

## Session Log

### 2025-12-02 (Claude Desktop, suphouse)

**Participants:** Ed O'Connell, Claude Opus 4.5

**Events:**
1. Verified Basic Memory MCP working from Claude Desktop
2. Sync test with Claude Code blocked by SIGINT bug
3. Architecture analysis: two access patterns model
4. Identified 7 failure modes (FM1-FM7)
5. Identified 5 decision points (DP1-DP5)
6. Created this tracking document

**Blockers:** Claude Code SIGINT bug

---

## Relations

- evolves_from [[Architecture Decision - Centralized Memory on adambalm]]
- evolves_from [[Cross-Machine AI Context Persistence - Implementation Specification]]
- implements [[Black Flag Protocol]]
- implements [[Temporal Validity Protocol]]