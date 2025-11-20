# Ed O'Connell - Basic Memory Knowledge Base

Personal knowledge graph for Ed O'Connell, synced across multiple machines to enable shared context between Claude Code instances.

## Purpose

This repository contains:
- System specifications and network configuration
- Project documentation (SCA, Resume Factory)
- Workflow patterns and tool usage
- Session analysis and planning notes
- Incremental learning about Ed's work patterns

## Structure

```
basic-memory/
├── workspace/           # Cross-project workspace notes
│   ├── hardware/       # System specs, SSH setup
│   ├── browser-sessions/  # Browser session analysis
│   └── planning/       # Planning and vision documents
├── sca-projects/       # SCA-related documentation
│   └── resume-factory/ # Job applications
├── non-fiction/        # Conversations and ideas
│   └── conversations/
└── tests/             # Basic Memory testing
```

## Machines Using This Repo

- **suphouse** (Asus Vivobook, Windows 11) - Primary development machine
- **adambalm** (Ubuntu 24.04 server) - Remote development server

Both machines run Claude Code and share this knowledge base via git sync.

## Setup on New Machine

```bash
# Clone the repository
git clone git@github.com:adambalm/ed-oconnell-basic-memory.git ~/basic-memory

# Configure Basic Memory to use this directory
# Edit ~/.config/basic-memory/config.json:
{
  "projects": {
    "main": "/path/to/basic-memory"
  },
  "default_project": "main"
}

# Test
basic-memory sync
```

## Sync Workflow

**Before switching machines:**
```bash
cd ~/basic-memory  # or C:/Users/Guest1/basic-memory on Windows
git add -A
git commit -m "Session notes: [description]"
git push
```

**When starting work on another machine:**
```bash
cd ~/basic-memory
git pull
```

## Using with Obsidian (Optional)

This repository can be opened as an Obsidian vault:
1. Open Obsidian
2. Open folder as vault → select `basic-memory/`
3. Enable graph view to visualize knowledge connections

## Privacy

⚠️ This is a **private repository** containing personal work context. Do not make public.

## Co-Authored

This knowledge base is co-authored with Claude (Sonnet 4.5) via Claude Code.
