---
title: Adambalm - Basic Memory Setup Instructions
type: note
permalink: workspace/hardware/adambalm-basic-memory-setup-instructions
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
