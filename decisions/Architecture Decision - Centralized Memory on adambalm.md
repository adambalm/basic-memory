---
title: Architecture Decision - Centralized Memory on adambalm
type: note
permalink: decisions/architecture-decision-centralized-memory-on-adambalm
status: canonical
temporal_type: dynamic
valid_from: 2024-11-26
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2024-11-26
tags:
- architecture
- basic-memory
- adambalm
- decision
- control-plane
---


## Summary

Established canonical architecture for cross-machine, multi-model AI memory system. All LLM queries route to adambalm as the single source of truth. Local machines maintain file copies via git for backup and offline browsing only.

## Decision Date
2025-11-26

## Status
Canonical

## Participants
- Ed O'Connell (Human Orchestrator)
- Claude Opus 4.5 (Architecture discussion)
- Claude Code (Diagnostics and verification)
- Gemini 2.0 Flash (Initial consultation - partially incorrect, prompted deeper investigation)

---

## Architecture

```mermaid
graph TD
    subgraph TAILNET
        subgraph ADAMBALM["ADAMBALM (Canonical Brain)"]
            API[Basic Memory HTTP API<br/>port 8765]
            DB[(SQLite Database)]
            FILES[Markdown Files<br/>/home/ed/basic-memory]
            OLLAMA[Ollama<br/>RTX 5060 Ti]
            
            API --> DB
            DB --> FILES
            OLLAMA -.->|future: embeddings| DB
        end
        
        SUPHOUSE[suphouse<br/>Windows]
        IMAC[iMac]
        MACPRO[Mac Pro]
        IPHONE[iPhone<br/>Termius]
        
        SUPHOUSE -->|HTTP queries| API
        IMAC -->|HTTP queries| API
        MACPRO -->|HTTP queries| API
        IPHONE -->|SSH to any machine| ADAMBALM
    end
    
    CLAUDE[Claude] -->|MCP or REST| API
    GEMINI[Gemini] -->|REST| API
    CHATGPT[ChatGPT] -->|REST| API
    LOCAL_OLLAMA[Ollama on adambalm] -->|localhost| API
```

---

## Key Decisions

- [decision] adambalm is the single source of truth for all AI memory queries #architecture
- [decision] Basic Memory HTTP server runs on adambalm port 8765 using streamable-http transport #infrastructure
- [decision] Other machines query adambalm over Tailnet; they do not run their own MCP servers #architecture
- [decision] Git sync retained for file backup and offline Obsidian browsing, not for database sync #operations
- [decision] Offline strategy is simple: browse files in Obsidian, use Cmd+Shift+F to search, wait for connectivity #operations
- [decision] No complex offline fallback or local database sync - overengineering for a rare use case #architecture

---

## Technical Specifications

### Server Command (adambalm)
```bash
~/.local/bin/uvx basic-memory mcp \
  --transport streamable-http \
  --port 8765 \
  --host 0.0.0.0
```

### Available Endpoints
- `/mcp` - MCP protocol (for Claude)
- `/main/search/` - REST search endpoint
- `/main/knowledge/entities` - Entity CRUD
- `/main/memory/recent` - Recent activity
- `/docs` - Swagger UI (interactive API docs)

### Client Configuration (suphouse, etc.)
```json
{
  "mcpServers": {
    "basic-memory-adambalm": {
      "type": "http",
      "url": "http://100.111.114.84:8765/mcp"
    }
  }
}
```

---

## Rationale

### Why Centralized?
- One source of truth eliminates sync conflicts
- Ollama on adambalm can generate embeddings locally (future)
- Vector store (future) lives on same machine as inference
- Simpler than distributed sync

### Why HTTP over MCP-only?
- MCP is Claude-ecosystem specific
- HTTP REST allows any LLM (Gemini, ChatGPT, Ollama) to access memory
- Standard protocol, no vendor lock-in

### Why Keep Git?
- Version control for rollback
- Backup if adambalm fails
- Human browsing in Obsidian without network dependency

---

## What This Enables (Control Plane Vision)

- [concept] Multi-model memory access - any LLM can query the same knowledge base #capability
- [concept] Decision logging with provenance - canonical record of what was decided and why #capability
- [concept] Protocol enforcement - Black Flag, Lanesborough accessible to all agents #capability
- [concept] Human approval gates - writes can require human sign-off #capability

---

## IMPLEMENTATION STATUS

**Updated:** 2025-11-26

### ✅ IMPLEMENTED

- [x] Protocols (Black Flag, Temporal Validity, Lanesborough) added to Basic Memory
- [x] Bootstrap document created (`BOOTSTRAP.md` with AI context loading instructions)
- [x] Git repository configured with GitHub remote (private repo)
- [x] MCP servers configured on both machines (stdio mode working)
- [x] Bidirectional git sync operational (push/pull workflow)
- [x] Frontmatter standardization complete across all documents

### ⏳ PENDING (Future Implementation)

- [ ] HTTP server not yet running persistently on adambalm
- [ ] No systemd service created for persistent HTTP server
- [ ] REST API not tested from non-Claude clients (Gemini, ChatGPT)
- [ ] Embedding/vector store integration (future phase)

### 📝 NOTE

Current implementation uses stdio MCP servers (local mode) with git-based sync.
HTTP server mode can be implemented when multi-client access is needed.

---

## Relations

- implements [[Cross-Machine AI Context Persistence - Implementation Specification]]
- supersedes distributed sync approach documented in that spec
- enables [[Lanesborough Protocol]] by providing shared context
- enables [[Black Flag Protocol]] by providing verifiable decision log
- runs_on [[Adambalm Server - Complete System Specifications]]
- accessed_from [[Suphouse (Asus Vivobook) - Complete System Specifications]]

---

## Context

This decision emerged from a troubleshooting session where:
1. Git repos had diverged between machines
2. Basic Memory databases were out of sync
3. Gemini consultation revealed misunderstandings about Black Flag and Lanesborough protocols
4. Investigation showed Basic Memory 0.16.2 has built-in HTTP server capability
5. Discussion clarified that the real value is the control plane (protocols, decisions, approvals), not the storage plumbing

The offline complexity we initially designed was overengineering. Simple git + Obsidian search is sufficient for rare offline scenarios.
