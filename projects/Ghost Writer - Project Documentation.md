---
title: Ghost Writer - Project Documentation
type: note
permalink: projects/ghost-writer-project-documentation
tags:
- project
- ocr
- handwriting
- supernote
- multi-agent
- provisional
- ghost-writer
---

# Ghost Writer - Project Documentation

---
type: project
status: paused
temporal_type: dynamic
valid_from: 2025-01-01
last_verified: 2025-12-04
tags:
- project
- ocr
- handwriting
- supernote
- multi-agent
- provisional
---

## Summary

Ghost Writer is an OCR and document processing system for handwritten notes, specifically designed to extract content from Supernote devices. The project reached a functional state (137 tests passing, 68% coverage) but is currently paused.

**Repository:** https://github.com/adambalm/ghost-writer (public)

---

## Architecture

```
Supernote Cloud → .note files (proprietary format)
       ↓
PNG rendering (reverse-engineered format parsing)
       ↓
Hybrid OCR Pipeline:
  - Qwen2.5-VL 7B (local, primary - 2-5s response)
  - Tesseract (local fallback)
  - Google Vision (premium accuracy)
  - GPT-4 Vision (semantic understanding)
       ↓
Relationship Detection → Concept Clustering → Structure Generation
       ↓
Output: Markdown, PDF, structured documents
```

### Key Technical Achievements

- [achievement] Working Supernote Cloud API integration with authentication #supernote
- [achievement] Hybrid OCR with intelligent cost-aware routing #ocr
- [achievement] Local-first processing with Qwen2.5-VL via Ollama #privacy
- [achievement] 137 tests passing, 68% code coverage #testing
- [achievement] Multi-agent coordination protocol (proto-Lanesborough) #architecture

---

## Multi-Agent Patterns (Proto-Lanesborough)

Ghost Writer implemented early versions of what became the Lanesborough Protocol:

### What Worked

| Pattern | Implementation | Outcome |
|---------|---------------|---------|
| Evidence tagging | `[verified]` vs `[inference]` labels | Clear epistemic status |
| Professional tone | "NEVER claim 'completely solved'" | Reduced false confidence |
| Commit discipline | Max 7 files, 300 lines, RISK/ROLLBACK/EVIDENCE | Auditable changes |
| Agent coordination | CLAUDE.md + AGENTS.md per-agent docs | Context preservation |

### What Needs Review

- HANDOFF_ARTIFACTS.md - Inter-agent communication log (needs inspection)
- AGENT_STATUS.md - Real-time state tracking (needs inspection)
- Document-based handoffs vs. shared memory - tradeoffs unclear

**Note:** These patterns predate Lanesborough Protocol formalization. Claude Code should review the full repo to extract lessons learned.

---

## Infrastructure Context

### Caddy Configuration Origin

The disabled Caddy config on adambalm (`ghost-writer` reference) originated from this project:

```caddy
https://adambalm.tail069d40.ts.net {
    tls internal
    root * /home/ed/ghost-writer
    # iOS certificate distribution
    # Proxies to ports 5001, 8001
}
```

### TLS/CA Situation (Probable Server Trauma Source)

Ghost Writer required iOS Safari to trust a development CA for Playwright testing:

- Created custom root CA: `ed-dev-root.mobileconfig`
- Purpose: Safari HTTPS-only mode compliance for UI testing
- Architecture: Playwright MCP on adambalm → visible browser on suphouse
- **This remote display + custom CA + Playwright combination is the likely source of past server instability**

The complexity was:
1. Playwright running on server (adambalm)
2. Browser UI needed on client (suphouse) for visual debugging
3. Safari's HTTPS requirements forced custom CA creation
4. Caddy configured for internal TLS on Tailscale domain

**Lesson:** Remote browser automation with custom CAs is fragile. The current Basic Memory TLS needs (simple reverse proxy) are much simpler.

---

## Current State

### What's Implemented ✅
- Supernote Cloud sync with authentication
- Hybrid OCR pipeline with local/cloud routing
- Relationship detection and concept clustering
- Structure generation (outlines, timelines, mindmaps)
- Comprehensive test suite
- Multi-agent development protocols

### What's Incomplete ⏳
- Storage and retrieval layer (never reached)
- Production deployment
- Long-term usage patterns

### Why Paused
- Core OCR functionality works
- Storage/retrieval scope undefined
- Other priorities (Basic Memory architecture, SCA work)

---

## Relevance to Current Work

### Patterns to Adopt for Multi-Model Memory Access

1. **Evidence tagging** → Already in Black Flag Protocol
2. **Commit discipline (RISK/ROLLBACK/EVIDENCE)** → Maps to merge agent audit logs
3. **Per-agent documentation** → Maps to per-model namespaces
4. **Professional communication standards** → Applies to all AI outputs

### Patterns to Evaluate

1. **Document-based handoffs** - Ghost Writer used files; Basic Memory could use notes
2. **AGENT_STATUS.md real-time tracking** - Could inform model activity monitoring
3. **Cost controls with fallbacks** - Relevant for API-based models

---

## Action Items

- [ ] Claude Code: Full repo review for additional patterns
- [ ] Extract HANDOFF_ARTIFACTS.md and AGENT_STATUS.md content
- [ ] Determine if project should resume or archive
- [ ] Decide on ghost-writer directory cleanup on adambalm (7.8GB)

---

## Relations

- explains [[adambalm Server Health Report - December 2025]] (Caddy config origin)
- precedes [[Lanesborough Protocol]] (early multi-agent patterns)
- precedes [[Black Flag Protocol]] (evidence tagging patterns)
- informs [[Multi-Model Write Access Governance]] (coordination patterns)
- runs_on [[Adambalm Server - Complete System Specifications]]
