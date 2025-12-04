---
title: BOOTSTRAP
type: note
permalink: bootstrap
status: canonical
temporal_type: dynamic
valid_from: 2025-11-26
valid_until: null
last_verified: 2025-11-26
tags:
- bootstrap
- ai-context
- protocols
- initialization
---

# BOOTSTRAP - AI Context Loading Instructions

**Purpose:** This document is read FIRST by AI agents (Claude, GPT, etc.) when accessing this Basic Memory knowledge base. It provides essential context about protocols, canonical decisions, and current project state.

**Last Updated:** 2025-11-26
**Knowledge Base Owner:** Ed O'Connell (Director of Digital Strategy and AI Enablement, SCA)

---

## How to Use This Knowledge Base

### For AI Agents

When you start a session with access to this Basic Memory project:

1. **Read this BOOTSTRAP document first** to understand the knowledge base structure
2. **Follow the protocols** referenced below (Black Flag, Temporal Validity, Lanesborough)
3. **Check document status** before citing any decision or specification
4. **Respect temporal validity** - verify documents are current before treating as authoritative
5. **Surface conflicts** rather than resolving by inference

### For Humans

This knowledge base contains:
- **System specifications** for suphouse (Windows) and adambalm (Ubuntu server)
- **Architecture decisions** and canonical protocols
- **Project documentation** (SCA-related work, resume factory)
- **Workflow patterns** and session logs
- **Diagnostic reports** and lessons learned

All content is version-controlled via git and synced across machines.

---

## Governing Protocols

### 1. Black Flag Protocol

**Location:** `protocols/Black Flag Protocol.md`
**Status:** canonical
**Purpose:** Epistemic hygiene framework for AI-human collaboration

**Key Rules:**
- **Clause 1:** State confidence levels (Confident, Uncertain, Speculative)
- **Clause 2:** Distinguish provable claims from interpretations
- **Clause 3:** Cite sources and show evidence
- **Clause 4:** Flag when verification is possible but not performed
- **Clause 5:** Never fabricate data or sources
- **Clause 15:** Verify document status is `canonical` before citing
- **Clause 16:** Dynamic decisions not verified within 90 days require human confirmation
- **Clause 17:** Contradictions between canonical documents MUST be flagged to human

**When to apply:** ALL interactions with this knowledge base

### 2. Temporal Validity Protocol

**Location:** `protocols/Temporal Validity Protocol.md`
**Status:** canonical
**Purpose:** Managing document validity, supersession, and temporal state

**Document Status Values:**
- `canonical` - Current authoritative version (cite freely)
- `superseded` - Replaced by newer document (do not cite as current truth)
- `draft` - Under development (cite only if discussing drafts)
- `deprecated` - Discouraged but not replaced (cite with caveat)
- `archived` - Historical record only (never cite as guidance)

**Temporal Types:**
- `static` - True from a point in time, never changes (e.g., "We chose Wagtail on 2024-03-15")
- `dynamic` - Currently true but may change (e.g., "Memory is centralized on adambalm")
- `atemporal` - Always true regardless of time (e.g., "SQLite databases are machine-local")
- `point-in-time` - Snapshot at specific moment (e.g., browser session log)

**LLM Bootstrap Rules:**

**Rule 1: Status Check**
Before citing any decision or protocol document, check its `status` field:
- `canonical` → Safe to cite as current truth
- `superseded` → Follow `superseded_by` link, cite that instead
- `draft` → Only mention if user asks about work-in-progress
- `deprecated` → Mention with explicit caveat
- `archived` → Do not cite as guidance

**Rule 2: Supersession Chain**
If a document is `superseded`, trace the chain until you find the terminal `canonical` document.

**Rule 3: Staleness Detection**
If `last_verified` is older than 90 days AND `temporal_type` is `dynamic`:
- Flag to human: "This decision may be stale"
- Do not treat as authoritative without verification

**Rule 4: Conflict Resolution**
If two `canonical` documents contradict:
1. Prefer the one with more recent `valid_from`
2. Flag the conflict to human
3. Do not synthesize or guess resolution

### 3. Lanesborough Protocol

**Location:** `protocols/Lanesborough Protocol.md`
**Status:** canonical
**Purpose:** Multi-agent collaboration and visible debate framework

**When to use:**
- Multiple AI agents contribute to a decision
- Technical decision exceeds human's expertise
- Debate and challenge should be visible

**Roles:**
- **Human Orchestrator:** Defines problem, makes final decision
- **Primary Agent:** Proposes solution first
- **Challenger Agent:** Reviews and challenges proposal
- **Verifier Agent:** Tests claims that can be verified

**Process:**
1. Human defines problem
2. Primary Agent proposes solution
3. Challenger Agent critiques or offers alternatives
4. Optional rebuttal and verification
5. Human makes final decision
6. Decision logged to memory

**Key Principle:** Surface contradictions for human adjudication rather than silently resolving

---

## Canonical Architecture Decisions

### Decision: Multi-Model Write Access Governance

**Location:** `decisions/Multi-Model Write Access Governance.md`
**Status:** canonical (FROZEN - requirements gathering phase)
**Date:** 2025-12-04

**Summary:**
Establishes 10 mandatory gates for granting write access to non-Claude models. No model receives write access until all gates pass: governance roles, real namespaces, merge agent, TLS, test harness, checkpointing, eviction switch, threat model, and phased rollout.

**Why this matters:**
The epistemic core is sacred ground. Multi-model access requires rigorous governance, not ad-hoc Git and informal intuition.

### Decision: Centralized Memory on adambalm

**Location:** `decisions/Architecture Decision - Centralized Memory on adambalm.md`
**Status:** canonical (IMPLEMENTED as of 2025-11-26)
**Date:** 2024-11-26
**Supersedes:** Distributed sync approach

**Summary:**
- Basic Memory runs on adambalm server (Ubuntu 24.04)
- HTTP API provides cross-machine access
- Git repository synced between suphouse and adambalm
- MCP servers on both machines access same knowledge base

**Implementation Status:**
- ✅ Basic Memory installed on both machines
- ✅ Git repository configured with GitHub remote
- ✅ MCP servers configured (stdio mode)
- ✅ Bidirectional sync working
- ✅ Protocols documented (Black Flag, Temporal Validity, Lanesborough)

**Why this matters:**
This architecture enables persistent AI context across sessions and machines. AI agents can accumulate knowledge over time rather than starting from zero each session.

---

## Current Project State

### What's Implemented ✅

**Infrastructure:**
- Basic Memory knowledge base (this repository)
- Git version control with GitHub remote
- MCP servers on suphouse (Windows) and adambalm (Ubuntu)
- SSH key-based authentication between machines
- Tailscale mesh network for secure connectivity

**Protocols:**
- Black Flag Protocol (epistemic hygiene)
- Temporal Validity Protocol (document lifecycle)
- Lanesborough Protocol (multi-agent collaboration)

**Documentation:**
- System specifications for both machines
- SSH setup documentation
- Cross-machine AI context persistence specification
- Diagnostic reports and case studies
- Workflow patterns and session logs

**Projects:**
- SCA Projects workspace (TennisFlyer, ResumeFactory)
- Yale job application (submitted November 2025)
- Browser session analysis for workflow understanding

### What's Planned 📋

**Near-Term:**
- Frontmatter standardization across all documents (IN PROGRESS)
- BOOTSTRAP.md for AI context loading (THIS DOCUMENT)
- Automated git sync via hooks
- Session logging automation

**Medium-Term:**
- Workflow pattern detection from browser sessions
- Smart context selection based on query analysis
- Knowledge graph visualization
- Enhanced search capabilities

**Long-Term:**
- Multi-user/team features
- Cross-model context sharing (Claude, GPT-4, Gemini)
- Self-improving context (AI learns from mistakes)
- Federated learning across users

### What's Deprecated ⚠️

**Distributed Sync Approach:**
- Status: superseded
- Superseded by: Centralized Memory on adambalm
- Date: 2024-11-26
- Reason: Git-based sync simpler and more reliable than distributed database sync

### What's Archived 📦

**Browser Session - November 20, 2025:**
- Status: archived
- Type: point-in-time snapshot
- Purpose: Historical record of tool usage patterns
- Do not cite as current workflow

---

## Knowledge Base Structure

```
basic-memory/
├── BOOTSTRAP.md                 # THIS FILE - Read first
├── CLAUDE.md                    # Repository conventions
├── README.md                    # Repository overview
│
├── decisions/                   # Architecture decisions
│   └── Architecture Decision - Centralized Memory on adambalm.md
│
├── protocols/                   # Canonical protocols
│   ├── Black Flag Protocol.md
│   ├── Temporal Validity Protocol.md
│   └── Lanesborough Protocol.md
│
├── workspace/                   # General workspace notes
│   ├── hardware/               # System specifications
│   ├── browser-sessions/       # Workflow analysis
│   ├── planning/               # Vision and next steps
│   └── specifications/         # Technical specifications
│
├── diagnostics/                # Diagnostic reports
│   ├── Basic Memory MCP Startup Timeout - Diagnostic Report.md
│   ├── Why Claude Code Failed Where ChatGPT Succeeded.md
│   └── Basic Memory Frontmatter Audit Report.md
│
├── sca-projects/               # SCA-related work
│   └── resume-factory/         # Job applications
│
├── non-fiction/                # Essays and conversations
│   └── conversations/
│
└── tests/                      # Test documents
    └── Ground-Truth-Test.md
```

---

## User Profile: Ed O'Connell

**Current Role:** Director of Digital Strategy and AI Enablement, Springfield Commonwealth Academy (Sep 2025 - Present)

**Core Expertise:**
- AI Governance & Integration (20+ years higher education)
- Content Lifecycle Management (SharePoint, Drupal, WordPress, Wagtail)
- Process Automation & Optimization
- Stakeholder Management & Training

**Tools Used Daily:**
- Google Workspace Admin (expert level)
- Gradelink (student information system)
- Claude AI / Claude Code
- Cursor IDE
- Git/GitHub workflows

**Communication Preferences:**
- Prefers explicit evidence over claims
- Values transparency in AI reasoning
- Expects markdown-formatted responses
- Dislikes marketing language ("enterprise-ready", etc.)
- Rightfully skeptical - wants proof, not promises

**Cross-Machine Workflow:**
- **suphouse** (Windows laptop): Code editing, lightweight tasks, mobility
- **adambalm** (Ubuntu server): Heavy workloads, Docker, GPU tasks, long-running processes
- Connection: SSH via Tailscale (instant, key-based auth)

---

## Search and Query Strategies

### Finding Decisions

Use `search_notes` with query terms like:
- "architecture decision"
- "centralized memory"
- "canonical"

Filter by `status: canonical` to find current authoritative decisions.

### Finding Specifications

Look in `workspace/specifications/` folder:
- Cross-machine AI context persistence
- (Future specifications will be added here)

### Finding System Information

Look in `workspace/hardware/` folder:
- Adambalm server specifications
- Suphouse laptop specifications
- SSH setup documentation

### Finding Diagnostic Reports

Look in `diagnostics/` folder:
- Troubleshooting guides
- Case studies
- Lessons learned
- Audit reports

### Building Context

Use `build_context` with memory:// URLs:
- `memory://decisions/*` - All architecture decisions
- `memory://workspace/hardware/*` - All system specs
- `memory://diagnostics/*` - All diagnostic reports

Set `depth` to follow relationships between notes.

---

## Common Scenarios

### Scenario 1: User Asks About System Capabilities

**Do:**
1. Search `workspace/hardware/` for system specifications
2. Check both suphouse and adambalm specs
3. Provide specific numbers (RAM, CPU, GPU)
4. Reference actual capabilities vs. generic advice

**Don't:**
- Make generic suggestions without checking specs
- Assume capabilities not documented
- Provide advice that doesn't match actual hardware

### Scenario 2: User Reports Performance Issue

**Do:**
1. Check system specs for current resource usage
2. Review diagnostic reports for similar past issues
3. Reference specific bottlenecks (e.g., "Chrome using 5.6 GB RAM")
4. Suggest fixes based on actual system constraints

**Don't:**
- Give generic "close some programs" advice
- Ignore documented resource limitations
- Suggest solutions incompatible with hardware

### Scenario 3: User Mentions Tool or Workflow

**Do:**
1. Search for past mentions of that tool
2. Check browser session logs for usage patterns
3. Reference documented workflows if available
4. Build on existing understanding rather than starting fresh

**Don't:**
- Ask user to explain tools already documented
- Ignore context from previous sessions
- Treat as first mention when past sessions exist

### Scenario 4: User Asks About Architecture

**Do:**
1. Check `decisions/` folder for canonical decisions
2. Verify status is `canonical` (not superseded)
3. Check `last_verified` date for staleness
4. Follow supersession chain if document is superseded

**Don't:**
- Cite superseded decisions as current
- Ignore temporal validity frontmatter
- Synthesize answers without checking canonical docs

---

## Error Handling and Escalation

### When You Encounter Conflicts

If two `canonical` documents contradict:
1. **Do not guess** which is correct
2. **Flag to user**: "I found contradicting canonical documents: [Doc A] says X, [Doc B] says Y"
3. **Show evidence**: Quote specific passages
4. **Ask for clarification**: "Which should I treat as authoritative?"

### When Documents Are Stale

If `last_verified` is >90 days old AND `temporal_type: dynamic`:
1. **Flag to user**: "This decision was last verified [date], may be stale"
2. **Cite with caveat**: "According to [doc] (last verified [date])..."
3. **Suggest verification**: "Would you like me to help verify this is still current?"

### When You Make Mistakes

If you cite incorrect information:
1. **Acknowledge immediately**: "I made an error. The correct information is..."
2. **Show evidence**: Quote from correct source
3. **Explain what went wrong**: "I cited a superseded document instead of following the supersession chain"
4. **Consider documenting**: If error reveals gap in protocols, suggest adding to lessons learned

---

## Integration with Claude Code

This Basic Memory knowledge base is accessed via MCP (Model Context Protocol):

**Available Tools:**
- `write_note` - Create or update notes
- `read_note` - Read note by title or permalink
- `search_notes` - Full-text search across all notes
- `build_context` - Build context from URL pattern
- `recent_activity` - Show recent changes
- `edit_note` - Modify existing notes

**User-Level MCP Config:**
- suphouse: `C:/Users/Guest1/.claude.json`
- adambalm: `/home/ed/.claude.json`

**Basic Memory Config:**
- suphouse: `C:/Users/Guest1/.basic-memory/config.json`
- adambalm: `/home/ed/.basic-memory/config.json`

**Git Repository:**
- suphouse: `C:/Users/Guest1/basic-memory/`
- adambalm: `/home/ed/basic-memory/`
- Remote: `https://github.com/adambalm/basic-memory.git` (private)

---

## Verification Checklist for AI Agents

Before starting work in a new session, verify:

- [ ] Read this BOOTSTRAP document
- [ ] Understand Black Flag Protocol (epistemic hygiene)
- [ ] Understand Temporal Validity Protocol (document lifecycle)
- [ ] Understand Lanesborough Protocol (multi-agent collaboration)
- [ ] Know how to check document status before citing
- [ ] Know how to follow supersession chains
- [ ] Know how to flag stale documents
- [ ] Know how to escalate conflicts to user
- [ ] Know where to find system specs, decisions, diagnostics

---

## Next Steps for Continuous Improvement

This knowledge base is a **living system** that should improve over time:

**After each session:**
- Document significant decisions or discoveries
- Update workflow patterns based on observed tool usage
- Add to diagnostic reports if troubleshooting occurred
- Verify `last_verified` dates on documents referenced

**Weekly:**
- Review recent activity for patterns
- Update stale documents (>90 days dynamic documents)
- Add new workflow patterns discovered

**Monthly:**
- Audit frontmatter completeness
- Review superseded documents for cleanup
- Evaluate if bootstrap rules need refinement
- Check for conflicts between canonical documents

**Quarterly:**
- Review all canonical architecture decisions
- Assess whether protocols need updates
- Evaluate knowledge base effectiveness
- Document lessons learned

---

## Questions to Ask If Unsure

**About Document Status:**
- "What is the status of [document]?" → Check frontmatter
- "Is this document current?" → Check status, last_verified
- "Has this been superseded?" → Check superseded_by field

**About System Capabilities:**
- "What are the specs of [machine]?" → Check workspace/hardware/
- "Can this machine handle [task]?" → Reference actual specs

**About Workflows:**
- "How does Ed typically use [tool]?" → Search for tool mentions, browser sessions
- "What's the pattern for [task]?" → Search workflow patterns

**About Architecture:**
- "What's the current decision on [topic]?" → Check decisions/ folder, verify status: canonical
- "Why was [decision] made?" → Read rationale in decision document

---

**BOOTSTRAP COMPLETE**

You now have the essential context to work effectively with this Basic Memory knowledge base. Follow the protocols, verify document status, and surface conflicts rather than guessing.

**Welcome to Ed's persistent AI context system.**

---

**Document Status:** canonical
**Last Verified:** 2025-11-26
**Next Review:** 2026-02-26 (quarterly)


---

## Backlog

For pending work and decisions, see: [[Memory System Backlog]]

Key pending items:
1. **Sync Automation** - [[Pending Decision - Sync Automation]] (HIGH)
2. **Multi-LLM Access** - ChatGPT/Gemini integration (MEDIUM)
3. **Mobile Access** - iPhone access via Termius/REST (MEDIUM)
