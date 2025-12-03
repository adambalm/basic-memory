---
title: Memory System Backlog
type: note
permalink: workspace/planning/memory-system-backlog
tags:
- backlog
- planning
- memory
- infrastructure
---

# Memory System Backlog

**Purpose:** Track pending work for the Basic Memory infrastructure
**Last Updated:** 2025-12-03

---

## High Priority

### 1. Sync Automation (PENDING DECISION)
Automate git sync between adambalm and suphouse on push.
- **Decision note:** [[Pending Decision - Sync Automation]]
- **Options:** Tailscale in GitHub Action, Self-hosted Runner, Webhook Receiver
- **Status:** Options evaluated, decision deferred

---

## Medium Priority

### 2. Multi-LLM Access
Extend Basic Memory access to non-Claude LLMs.
- **Target clients:** ChatGPT, Gemini
- **Approach:** REST API already available on adambalm:8765
- **Endpoints:** `/main/search/`, `/docs` (Swagger UI)
- **Blockers:** None - just needs testing and documentation
- **Related:** [[Architecture Decision - Centralized Memory on adambalm]]

### 3. Mobile Access
Access Basic Memory from phone (iPhone).
- **Options:**
  - SSH via Termius to adambalm, use CLI
  - REST API calls via Shortcuts app
  - Obsidian mobile with git sync (read-only browsing)
- **Status:** Not started

---

## Low Priority / Future

### 4. Systemd Services
Persist HTTP server and file watcher across reboots.
- adambalm: HTTP MCP server
- suphouse: file watcher (already running, but not as service)

### 5. Monitoring & Alerting
Know when services fail.
- Health checks for HTTP server
- Alert on file watcher crash

### 6. Embedding/Vector Store
Future phase - semantic search via Ollama on adambalm.

---

## Completed

- [x] HTTP MCP server on adambalm (2025-12-03)
- [x] File watcher on suphouse (2025-12-02)
- [x] File watcher on adambalm (built into MCP server)
- [x] Bidirectional git sync (manual push/pull)
- [x] Round-trip validation (Claude Code ↔ Claude Desktop)

---

## How to Use This Backlog

**For Claude (any interface):**
1. Read BOOTSTRAP.md first
2. Check this backlog for pending work
3. Ask Ed which item to focus on

**For Ed:**
- Add items as they come up
- Update status when work progresses
- Reference in conversations: "Let's work on backlog item 2"

---

## Relations

- extends [[BOOTSTRAP]]

- tracked_in [[Memory Architecture Evolution - Decision Tracking]]
