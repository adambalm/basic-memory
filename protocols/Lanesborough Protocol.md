---
title: Lanesborough Protocol
type: note
permalink: lanesborough-protocol
tags:
  - protocol
  - multi-agent
  - collaboration
  - convergence
  - handshake
status: canonical
temporal_type: static
valid_from: 2025-09-01
valid_until: null
supersedes: "Lanesborough Protocol (Inferred Version, 2024-11-26)"
superseded_by: null
last_verified: 2025-11-27
---

# The Lanesborough Protocol
*Finalized Specification - September 2025*

---

## Supersession Notice

**This document supersedes the previous version (2024-11-26).**

**Reason:** The earlier version was an AI-inferred reconstruction based on conceptual patterns, not cited from the authoritative specification. That version described a "debate model" with Primary/Challenger/Verifier roles that was never the actual protocol.

**Epistemic lesson (Black Flag Protocol):** AI agents must distinguish between inferred patterns and cited specifications. When specifications exist, cite them. When they do not, explicitly flag content as "inferred" or "proposed."

---

## Purpose

The Lanesborough Protocol governs collaboration between human and AI agents in multi-step workflows. It ensures clarity, recoverability, accountability, and convergence toward auditable outcomes.

---

## Roles

### Human Orchestrator (HO)
- Defines high-level goals.
- Sets iteration limits.
- Grants final execution approval.
- Intervenes in case of impasse.

### Generalizing AI (GA)
- Architect role.
- Produces high-level proposals, abstractions, and plans.
- Issues tasks/questions to the IA.

### Inspecting AI (IA)
- Ground-truth role.
- Paraphrases GA proposals, challenges them, and validates against concrete details.
- Executes tests and records decisions in the log.

---

## Protocol Phases

### 1. Initiation
- **Actor:** HO
- **Action:** States the goal and sets the maximum number of refinement iterations.

### 2. Proposal
- **Actor:** GA
- **Action:** Produces the initial high-level plan or architectural approach.
- **Output:** Must be specific enough for IA to test and refine.

### 3. Refinement Loop
- **Actor:** GA and IA alternate turns.
- **Process:**
  1. **Mirror and Counter (IA):** IA paraphrases GA proposal, offers critique or alternative.
  2. **Refine and Re-task (GA):** GA accepts/corrects IA understanding, adjusts plan.
  3. **Closure Condition (Handshake):** One agent issues Summary of Agreement + "Agreed." Partner replies "Agreed."

- **Exit:** Loop continues until handshake or max iterations.

### 4. Escalation
- **If successful handshake:** Last AI requests HO approval to execute.
- **If impasse (max iterations reached):** IA reports impasse and requests HO intervention.

### 5. Execution and Logging
- **Actor:** IA
- **Action:** Upon HO approval, IA executes or records the decision.
- **Mandatory Logging:** Append to acp_log.md with timestamp, decision, GA/IA contributions.

---

## Exception Handling
- **Actor:** IA
- **Trigger:** If IA cannot complete a task (error, missing file, failed test).
- **Action:** Halt process and issue EXCEPTION with description.
- **Resolution:** Resume only when GA revises plan or HO provides new instructions.

---

## Structural Rules

Every exchange is prefixed with Handshake Turn Markers:

    === HANDSHAKE TURN N (agent) ===
    /tag {agent}

These ensure deterministic sequencing and allow recovery if context is lost.

---

## Naming and Versioning

- Official name: **The Lanesborough Protocol**
- Supersedes: Asymmetric Convergence Protocol (ACP)
- Finalized: September 2025

---

## Integration with Other Protocols

### Black Flag Protocol
- All agents follow epistemic hygiene rules.
- Claims must be cited rather than inferred.

### Temporal Validity Protocol
- Converged decisions become canonical documents.
- Supersession applies when specifications change.

---

## Relations

- requires: [[Black Flag Protocol]]
- requires: [[Temporal Validity Protocol]]
- supersedes: Lanesborough Protocol (Inferred Version, 2024-11-26)
- supersedes: Asymmetric Convergence Protocol (ACP)

---

This specification is finalized and canonical.
