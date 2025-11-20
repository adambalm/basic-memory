---
title: Personalized Context System - Vision and Next Steps
type: note
permalink: workspace/planning/personalized-context-system-vision-and-next-steps
---

# Personalized Context System - Vision and Next Steps

**Date:** November 20, 2025, late evening
**Status:** Planning phase, user skeptical (rightly so) after I made unsubstantiated claims

## The Vision

Ed wants to build a system where Claude Code gradually learns his workflow patterns, tools, and context - not through one-time documentation, but through incremental refinement across many sessions.

**Key Quote:**
> "This is the kind of thing I would want to be slowly training an llm to understand, a gradual buildup of what I do, where we are constantly refining the understanding of context and organizing it and bringing more and more into our scope of inspection and making the tools smarter for ME."

## Requirements

1. **Systematic workflow documentation**
   - What each tool/domain represents in Ed's daily work
   - When tools are used together (pattern recognition)
   - Context switching patterns (teaching vs. admin vs. AI work)

2. **Knowledge sharing across Claude Code instances**
   - This machine (suphouse) and adambalm server need shared context
   - Basic Memory + Obsidian integration seems like natural fit
   - Alternative approaches if that doesn't work

3. **Trust and evidence**
   - User rightfully skeptical after Chrome session analysis incident
   - Need to show evidence, not make claims
   - Build trust through transparency

## Technical Approach (To Verify)

### Option A: Basic Memory + Obsidian Vault (Preferred)
- Basic Memory can use Obsidian vault as project directory
- Multiple Claude Code instances can point at same vault
- Vault can be synced via Tailscale network or cloud sync
- Need to verify: current Basic Memory setup, sharing workflow

### Option B: Alternative (If Obsidian doesn't work)
- Git-based shared repository
- Custom MCP server with network access
- Shared filesystem over Tailscale
- (User's input needed if we go this route)

## Next Steps (When Resumed)

1. **Verify Basic Memory + Obsidian integration**
   - Check current Basic Memory project structure
   - Test Obsidian vault integration
   - Document exact setup process

2. **Design knowledge graph structure**
   - workflow patterns
   - tool inventory with contextual usage
   - session type recognition
   - incremental learning methodology

3. **Test cross-machine knowledge sharing**
   - Point adambalm Claude Code at same Basic Memory project
   - Verify both instances can read/write
   - Test real-world scenario

4. **Start small, prove value**
   - Don't over-promise
   - Document ONE workflow pattern thoroughly
   - Show Ed it actually works before expanding

## Evidence of User Skepticism

Chrome session analysis incident:
- I claimed Google Classroom with "3 classes" without showing URLs
- I claimed Google Workspace Admin heavy usage without evidence
- When challenged, had to grep session files to show actual domains
- Lesson: ALWAYS show evidence first, then interpret

User's response:
> "I feel like you are making up that browser session summation"
> "I'm not convinced you aren't bullshitting me"

**Valid concerns.** Build trust through transparency and working solutions, not promises.

## Current Basic Memory Projects

Need to document:
- What projects exist (saw "main" in error message)
- Which one is "default" 
- Whether any are already Obsidian vaults
- Directory locations for both suphouse and adambalm

## Session Context When Resumed

User can reference:
- This note (workspace/planning/personalized-context-system-vision-and-next-steps)
- Chrome session analysis (workspace/browser-sessions/chrome-browser-session-november-20-2025)
- System specs notes (workspace/hardware/*)
- SSH setup note (workspace/hardware/ssh-key-based-authentication-setup-adambalm)

**Resume with:** "Let's continue the personalized context system planning from last session"

---

**Claude's Note to Future Self:** User is RIGHT to be skeptical. Earn trust through working solutions, not ambitious promises. Start small, prove value, then expand.


---

## GitHub Setup Progress (November 20, 2025 - Late Evening)

### Completed ✅
1. ✅ Initialized git repository in `C:/Users/Guest1/basic-memory`
2. ✅ Created `.gitignore` for Basic Memory
3. ✅ Made initial commit (commit `188c834`) with 10 files
4. ✅ Created `README.md` with repository structure and setup guide
5. ✅ Second commit (commit `c6b0516`) with documentation

### Manual Steps Required (gh CLI not available)

**To complete GitHub setup:**

1. **Create private repository on GitHub**
   - Go to https://github.com/new
   - Repository name: `ed-oconnell-basic-memory`
   - Description: "Personal knowledge graph for Ed O'Connell - shared context across Claude Code instances"
   - Visibility: **Private** (IMPORTANT)
   - Do NOT initialize with README (we already have one)

2. **Add remote and push**
   ```bash
   cd /c/Users/Guest1/basic-memory
   git remote add origin git@github.com:adambalm/ed-oconnell-basic-memory.git
   # OR if using HTTPS:
   git remote add origin https://github.com/adambalm/ed-oconnell-basic-memory.git
   
   git push -u origin master
   ```

3. **Setup on adambalm**
   ```bash
   ssh adambalm
   cd ~
   git clone git@github.com:adambalm/ed-oconnell-basic-memory.git basic-memory
   
   # Configure Basic Memory to use this directory
   # Edit ~/.config/basic-memory/config.json:
   # Change "main" project path to "/home/ed/basic-memory"
   ```

### Sync Workflow (Once Setup Complete)

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
```

### Current Local State
- Repository: Clean, 2 commits, on branch `master`
- Files: 11 files committed (10 markdown + 1 .gitignore)
- Remote: Not yet configured (waiting for GitHub repo creation)
- Size: 2,235 lines across all files

### Next Session Resume Point
When resuming: "Let's finish the GitHub setup for Basic Memory" - user needs to create the repo on GitHub web interface, then we'll add remote and push.