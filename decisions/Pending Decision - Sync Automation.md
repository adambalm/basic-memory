---
title: Pending Decision - Sync Automation
type: decision
permalink: decisions/pending-decision-sync-automation
status: draft
temporal_type: dynamic
valid_from: 2025-12-03
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-12-04
tags:
- pending
- decision
- sync
- ci-cd
- automation
- backlog
---

# Pending Decision - Sync Automation

**Status:** PENDING - Decision deferred 2025-12-03
**Priority:** High
**Context:** Ed was too tired to decide; resume next session

---

## The Problem

Basic Memory runs on adambalm (canonical). Git sync to suphouse is currently manual:
- Push from one machine
- Pull on the other
- File watcher auto-reindexes

We want automated sync on git push.

---

## Options Evaluated

### Option 1: Tailscale in GitHub Action
- GitHub runner installs Tailscale, SSHs to machines, runs git pull
- **Setup:** Medium (auth key + workflow YAML)
- **Maintenance:** Low (rotate key every 90 days)
- **Speed:** 30-60 seconds
- **Recommended starting point** - no daemons, no exposed ports

### Option 2: Self-hosted Runner
- GitHub Actions runner daemon on adambalm
- **Setup:** Medium
- **Maintenance:** Medium (monitor daemon)
- **Speed:** 10-20 seconds
- **Overkill** for just git pull

### Option 3: Webhook Receiver
- Simple HTTP listener on adambalm, GitHub sends POST on push
- **Setup:** Easy (~20 line script)
- **Maintenance:** Low
- **Speed:** 5-10 seconds (fastest)
- **Requires** exposed port (Tailscale Funnel)

---

## Recommendation

Start with Option 1 (Tailscale in Action). Upgrade to Option 3 if speed matters.

---

## To Resume This Decision

1. Read this note
2. Ask Ed which option he prefers
3. Implement the chosen option
4. Update this note to status: IMPLEMENTED

---

## Relations

- extends [[Architecture Decision - Centralized Memory on adambalm]]
- tracked_in [[Memory Architecture Evolution - Decision Tracking]]
