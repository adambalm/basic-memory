---
title: Adambalm - Basic Memory Setup Instructions
type: documentation
permalink: workspace/hardware/adambalm-basic-memory-setup-instructions
status: completed
temporal_type: static
valid_from: 2025-11-24
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-11-26
tags:
  - setup
  - adambalm
  - basic-memory
  - instructions
---

# Adambalm - Basic Memory Setup Instructions

**Purpose:** Configure adambalm server to use the shared Basic Memory GitHub repository  
**Repository:** https://github.com/adambalm/basic-memory  
**Status:** Suphouse setup complete, adambalm setup pending

---

## Prerequisites

- ✅ SSH access to adambalm configured (ssh key-based authentication)
- ✅ GitHub repository created and pushed from suphouse
- ✅ adambalm has git installed (Ubuntu 24.04)
- ⏳ Basic Memory installed on adambalm (need to verify)

---

## Setup Steps

### 1. Clone the Repository

```bash
ssh adambalm

# Clone to home directory
cd ~
git clone https://github.com/adambalm/basic-memory.git basic-memory

# Verify contents
cd ~/basic-memory
ls -la

# Expected structure:
# - workspace/
# - sca-projects/
# - non-fiction/
# - tests/
# - README.md
# - SETUP-COMPLETE-NEXT-STEPS.md
# - .gitignore
```

### 2. Check Basic Memory Installation

```bash
# Check if Basic Memory is installed
which basic-memory

# Check configuration location
ls -la ~/.config/basic-memory/

# View current config (if exists)
cat ~/.config/basic-memory/config.json
```

### 3. Configure Basic Memory to Use Git Repository

**If Basic Memory is already installed:**

```bash
# Edit configuration
nano ~/.config/basic-memory/config.json

# Update the "main" project path:
{
  "projects": {
    "main": "/home/ed/basic-memory"
  },
  "default_project": "main",
  "default_project_mode": false
}
```

**If Basic Memory is NOT installed:**

```bash
# Install Basic Memory (check official docs for latest method)
# Typically via pip or uv:
pip install basic-memory
# or
uv tool install basic-memory

# Then configure as above
```

### 4. Test Basic Memory Access

```bash
# Start Claude Code on adambalm
cd ~/basic-memory
claude

# In Claude Code session, ask Claude to:
# "Read the planning note about personalized context system"
# Should be able to read workspace/planning/Personalized Context System - Vision and Next Steps.md
```

### 5. Setup Git User (If Not Already Configured)

```bash
# Check current git config
git config --global user.name
git config --global user.email

# If not set or showing wrong user:
git config --global user.name "Ed O'Connell"
git config --global user.email "your-email@example.com"
```

---

## Daily Workflow on Adambalm

### Starting a Session

```bash
ssh adambalm
cd ~/basic-memory

# Pull latest changes from suphouse
git pull

# Start Claude Code
claude
```

### Ending a Session

```bash
cd ~/basic-memory

# Check what changed
git status

# Commit changes (if any)
git add -A
git commit -m "Session on adambalm: [description]"

# Push to GitHub
git push

# Exit
exit
```

---

## Sync Between Machines

**Pattern:**
1. **End session on Machine A:** commit + push
2. **Start session on Machine B:** pull first
3. **Work on Machine B:** Basic Memory auto-saves
4. **End session on Machine B:** commit + push
5. **Return to Machine A:** pull before starting work

**Avoid merge conflicts:**
- Always pull before starting work
- Always commit and push when ending session
- Don't leave uncommitted changes when switching machines

---

## Verification Checklist

After setup, verify:

- [ ] Repository cloned to `~/basic-memory`
- [ ] Basic Memory installed on adambalm
- [ ] Basic Memory config points to `~/basic-memory`
- [ ] Can read notes via Claude Code on adambalm
- [ ] Git user configured correctly
- [ ] Can pull/commit/push successfully
- [ ] Same notes visible on both suphouse and adambalm

---

## Troubleshooting

**Issue: Basic Memory can't find project**
```bash
# Check config
cat ~/.config/basic-memory/config.json

# Verify path is correct
ls -la ~/basic-memory

# Test Basic Memory directly
basic-memory list-directory --project main
```

**Issue: Git authentication fails**
```bash
# If using HTTPS, may need to cache credentials:
git config --global credential.helper cache

# Or set up SSH keys for GitHub
ssh-keygen -t ed25519 -C "your-email@example.com"
cat ~/.ssh/id_ed25519.pub
# Add to GitHub: https://github.com/settings/keys
```

**Issue: Permission denied on git operations**
```bash
# Check repository ownership
ls -la ~/basic-memory

# Should be owned by 'ed' user
# If not:
sudo chown -R ed:ed ~/basic-memory
```

---

## Current State

**Suphouse (Windows):**
- ✅ Repository: `C:/Users/Guest1/basic-memory`
- ✅ Remote: `https://github.com/adambalm/basic-memory`
- ✅ Status: Pushed, up to date
- ✅ Commits: 4 commits (initial + README + setup guide + planning updates)

**Adambalm (Ubuntu):**
- ⏳ Repository: Not yet cloned
- ⏳ Basic Memory: Installation status unknown
- ⏳ Configuration: Not yet set up

**Next Action:** SSH to adambalm and follow setup steps above

---

## Resume Instructions

To complete adambalm setup in next session:

```
"Let's set up Basic Memory on adambalm using the GitHub repository"
```

Claude will:
1. SSH to adambalm
2. Clone the repository
3. Check/configure Basic Memory
4. Verify sync works both directions
5. Test reading notes via Claude Code on adambalm


---

## ✅ Setup Complete (November 20, 2025)

### What Was Done

1. **Installed uv (v0.9.10)** on adambalm at `/home/ed/.local/bin/`
2. **Cloned Basic Memory repository** to `/home/ed/basic-memory` via git SSH
3. **Configured MCP server** in `~/.claude.json`:
   ```json
   "mcpServers": {
     "basic-memory": {
       "type": "stdio",
       "command": "/home/ed/.local/bin/uvx",
       "args": ["basic-memory", "mcp"],
       "env": {}
     }
   }
   ```
4. **Created config file** at `~/.basic-memory/config.json` pointing to `/home/ed/basic-memory`
5. **Verified installation**:
   - Repository: 12 files detected (README, setup docs, workspace/, sca-projects/, etc.)
   - CLI working: `uvx basic-memory status` shows project structure
   - MCP configured: Ready for Claude Code access

### Current State

**Repository:**
- Location: `/home/ed/basic-memory`
- Branch: master
- Files: 12 markdown files across workspace/, sca-projects/, non-fiction/, tests/
- Git remote: `git@github.com:adambalm/basic-memory.git`

**Basic Memory:**
- CLI: `/home/ed/.local/bin/uvx basic-memory`
- Config: `~/.basic-memory/config.json`
- Project: `main` → `/home/ed/basic-memory`
- Status: Installed, files detected, auto-indexing in progress

**MCP Server:**
- Configured in user-level `~/.claude.json`
- Command: `/home/ed/.local/bin/uvx basic-memory mcp`
- Will be available to all Claude Code sessions on adambalm

### Testing Results

```bash
# Status check (successful)
$ uvx basic-memory status --project main
├── README.md/ +1 new
├── SETUP-COMPLETE-NEXT-STEPS.md/ +1 new
├── non-fiction/ +1 new
├── sca-projects/ +2 new
├── tests/ +1 new
└── workspace/ +6 new

# CLI commands working
$ uvx basic-memory tool search-notes 'test' --project main
# (Returns results once indexing completes)
```

### Next Claude Code Session on Adambalm

When you start Claude Code on adambalm, Basic Memory MCP will automatically be available. You can:

```
# Ask Claude to read notes
"Show me the planning note about personalized context system"

# Search across knowledge base
"Search Basic Memory for SSH setup instructions"

# Create new notes
"Document this session in Basic Memory under workspace/sessions/"
```

### Sync Workflow Now Active

**On suphouse (ending session):**
```bash
cd /c/Users/Guest1/basic-memory
git add -A
git commit -m "Session: [description]"
git push
```

**On adambalm (starting session):**
```bash
cd ~/basic-memory
git pull
# Basic Memory auto-detects changes and re-indexes
```

### Verification Checklist

- [x] uv installed and working
- [x] Basic Memory CLI functional
- [x] Repository cloned with all files
- [x] Config.json created and pointing to repo
- [x] MCP server configured in Claude config
- [x] Files detected by Basic Memory status command
- [x] Git remote configured and accessible
- [ ] Files fully indexed (in progress - happens automatically)
- [ ] Tested via Claude Code MCP (pending next Claude Code session on adambalm)

### Troubleshooting Notes

**If Basic Memory doesn't find notes:**
- Files are auto-indexed in background
- Check status: `uvx basic-memory status --project main`
- Give it a few minutes for initial indexing
- Search will work once indexing completes

**If MCP not available in Claude Code:**
- Restart Claude Code session
- Check `~/.claude.json` has mcpServers.basic-memory configured
- Verify path: `/home/ed/.local/bin/uvx` exists and is executable

**If git sync fails:**
- Check SSH keys: `ssh -T git@github.com`
- Verify remote: `git remote -v` in ~/basic-memory
- Ensure you pushed from suphouse before pulling on adambalm

---

**Setup Time:** ~10 minutes
**Status:** ✅ Complete and functional
**Both machines now sharing Basic Memory via GitHub**