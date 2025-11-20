# CLAUDE.md - Basic Memory Repository Conventions

**Repository Type:** Personal Knowledge Base
**Owner:** Ed O'Connell
**Purpose:** Persistent AI context shared across machines via git
**Last Updated:** November 20, 2025

---

## File Naming Conventions

### Standard: kebab-case for all files

**Format:** `lowercase-with-hyphens.md`

**✅ Good:**
- `cross-machine-ai-context-persistence.md`
- `adambalm-server-specifications.md`
- `ssh-key-authentication-setup.md`

**❌ Bad:**
- `Cross Machine AI Context.md` (spaces, capitals)
- `adambalm_server_specs.md` (underscores)
- `SSH-Key-Setup.md` (mixed case)

**Why:**
- No quotes needed in CLI: `cat workspace/hardware/adambalm-server-specifications.md`
- Matches Basic Memory permalinks (auto-generated as kebab-case)
- Standard in web URLs and technical documentation
- Cross-platform compatible (Windows, Linux, macOS)

### Exceptions

**ALL CAPS for meta-documentation:**
- `README.md` - Repository overview
- `CLAUDE.md` - This file (conventions for AI)
- `SETUP-COMPLETE-NEXT-STEPS.md` - Setup guide

**Reason:** Standard convention, easily distinguishable from content files

---

## Directory Structure

```
basic-memory/
├── workspace/              # General workspace notes
│   ├── hardware/          # System specs, SSH, network
│   ├── browser-sessions/  # Browser session analysis
│   ├── planning/          # Planning and vision docs
│   └── specifications/    # Technical specifications
├── sca-projects/          # SCA-specific work
│   └── resume-factory/    # Job applications
├── non-fiction/           # Essays, conversations
│   └── conversations/
└── tests/                 # Test documents
```

**Guidelines:**
- Keep hierarchy shallow (max 3 levels deep)
- Use descriptive folder names (kebab-case)
- Group related notes together
- Don't create folders for single files

---

## Writing Style for Notes

### Be Specific and Evidence-Based

**✅ Good:**
```markdown
## Chrome Memory Usage (November 20, 2025)

Observed via PowerShell Get-Process:
- 82 processes consuming 5.6 GB RAM
- Primary domains: admin.google.com, gradelink.com, chatgpt.com
- Closing Chrome freed ~5.6 GB (dropped from 83% to 60% RAM usage)
```

**❌ Bad:**
```markdown
## Browser Issues

Chrome uses too much memory. This is a problem.
It makes the system slow.
```

**Why:**
- Specific data enables future reference
- Evidence prevents "hallucination" by AI
- Dates provide context for when observations were made

### No Marketing Language

**Avoid:**
- "enterprise-ready"
- "production-ready"
- "fully operational"
- "industry-leading"
- "best-in-class"

**Use instead:**
- Specific metrics: "handles 1000 requests/second"
- Test results: "passed 47/50 tests"
- Known limitations: "works on Ubuntu 24.04, untested on other distros"

**Why:** Ed specifically dislikes unsubstantiated claims. Be honest about status and limitations.

---

## Git Workflow

### Commit Message Format

```
type(scope): brief description

Longer explanation if needed (optional)

Co-Authored-By: Claude <noreply@anthropic.com>
```

**Types:**
- `feat` - New feature or capability
- `fix` - Bug fix
- `docs` - Documentation changes
- `chore` - Maintenance (dependency updates, etc.)
- `refactor` - Code restructuring without behavior change

**Scopes:**
- `workspace` - General workspace notes
- `sca` - SCA-specific projects
- `hardware` - System specifications
- `setup` - Configuration and setup

**Examples:**
```
docs(workspace): add cross-machine AI context specification
feat(sca): document Wagtail CMS project structure
fix(hardware): correct adambalm RAM specs (64GB not 32GB)
chore(setup): update Basic Memory to v0.5.2
```

### When to Commit

**Always commit after:**
- Completing a session (before switching machines)
- Creating new specification or major document
- Significant updates to existing notes
- Configuration changes

**Commit message should:**
- Start with lowercase (except proper nouns)
- Be concise but descriptive
- Explain *what* and *why*, not *how*

---

## Basic Memory Usage

### Tool Naming

When referencing Basic Memory MCP tools in documentation:

**Correct format:**
```
mcp__basic-memory__write_note
mcp__basic-memory__read_note
mcp__basic-memory__search_notes
```

**Not:**
- `basic-memory.write_note` (wrong separator)
- `writeNote` (wrong format)
- `write-note` (missing namespace)

### Note Identifiers

**Permalink (preferred):**
```
workspace/hardware/adambalm-server-specifications
```

**Title (also works):**
```
Adambalm Server - Complete System Specifications
```

**In practice:** Permalink is more reliable because it's kebab-case and won't change even if title is updated.

---

## What Belongs in This Repository

### ✅ Include

**System Context:**
- Hardware specifications for all machines
- Network configuration (Tailscale, SSH)
- Development environment setup

**Workflow Patterns:**
- Tool usage patterns (when Ed uses Gradelink + Classroom together)
- Common task sequences
- Context switches (teaching → admin → development)

**Project Documentation:**
- Project analysis and planning
- Session logs and progress tracking
- Technical decisions and rationale

**Learning Notes:**
- Concepts Ed is learning
- Tutorials and guides followed
- Skills assessment and progression

### ❌ Exclude

**Secrets:**
- API keys, passwords, tokens
- Private SSH keys (public keys OK)
- Database credentials
- OAuth tokens

**Sensitive Personal Info:**
- Financial information
- Medical records
- Social security numbers
- Student data (use anonymized examples only)

**Generated Artifacts:**
- Database files (*.db, *.sqlite)
- Build artifacts
- Large binary files
- Temporary files

**Why:** This is a private repo but still should follow security best practices. Secrets should be in environment variables or password managers, not git.

---

## AI Interaction Guidelines

### What AI Should Do

1. **Always cite sources** - Reference specific notes when making claims
2. **Admit uncertainty** - Say "I don't have a note about X" rather than guessing
3. **Show evidence** - Quote relevant sections from notes
4. **Ask for clarification** - When ambiguous, ask rather than assume
5. **Update notes proactively** - When learning new patterns, suggest note creation

### What AI Should NOT Do

1. **Hallucinate details** - Don't make up specifics not in notes
2. **Use marketing speak** - See "No Marketing Language" above
3. **Claim certainty without evidence** - Qualify statements appropriately
4. **Ignore user corrections** - When corrected, document the correction
5. **Over-promise** - Be realistic about capabilities and limitations

### Example Exchange

**Good:**
```
User: What's the RAM on adambalm?
AI: According to workspace/hardware/adambalm-server-specifications,
adambalm has 64GB RAM (DDR4). This was documented on November 20, 2025.
```

**Bad:**
```
User: What's the RAM on adambalm?
AI: Adambalm is a powerful server with enterprise-grade memory
configuration optimized for production workloads.
(No specific amount, marketing language, no source citation)
```

---

## Session End Checklist

Before ending any Claude Code session where notes were created or updated:

- [ ] Review changes: `git status`
- [ ] Stage all files: `git add -A`
- [ ] Commit with descriptive message: `git commit -m "type(scope): description"`
- [ ] Push to GitHub: `git push`
- [ ] Verify push succeeded: Check for "To https://github.com/adambalm/basic-memory.git"

**On next machine:**
- [ ] Pull latest: `git pull`
- [ ] Check Basic Memory status: `uvx basic-memory status --project main`
- [ ] Wait for indexing to complete (if needed)

---

## Troubleshooting

### "Note not found" in Basic Memory

**Possible causes:**
1. Note hasn't been indexed yet (wait 30 seconds, try again)
2. Using wrong identifier (try permalink instead of title)
3. File not committed to git (check `git status`)

**Fix:**
```bash
# Force re-index
uvx basic-memory reset --project main
```

### Git merge conflicts

**If you forgot to pull before working:**
```bash
git status  # Shows conflicts
git diff    # Shows conflicting changes
# Edit files to resolve conflicts
git add <resolved-files>
git commit -m "merge: resolve conflicts"
git push
```

**Prevention:** Always pull before starting work on a different machine.

### File name with spaces causes issues

**Problem:** Tab completion doesn't work, CLI commands fail

**Fix:**
```bash
# Rename to kebab-case
git mv "File With Spaces.md" "file-with-spaces.md"
git commit -m "refactor: standardize filename to kebab-case"
git push
```

---

## Metrics to Track (Optional)

To measure if this system is actually improving AI understanding:

**Quantitative:**
- Number of times user has to re-explain same concept
- Sessions where AI successfully references past conversations
- Reduction in clarification questions from AI

**Qualitative:**
- Does AI "feel" like it understands Ed's setup better?
- Are suggestions more relevant over time?
- Is there less frustration with context loss?

**Method:** After 30 days of daily use, review and assess whether system is valuable.

---

## References

**Documentation:**
- Full specification: `workspace/specifications/cross-machine-ai-context-persistence-implementation-specification.md`
- Setup guide: `workspace/hardware/adambalm-basic-memory-setup-instructions.md`
- Planning vision: `workspace/planning/personalized-context-system-vision-and-next-steps.md`

**External:**
- Basic Memory: https://github.com/basicmachines-co/basic-memory
- MCP Protocol: https://github.com/modelcontextprotocol
- Git best practices: https://git-scm.com/book

---

**End of Conventions**

**Note to AI:** This file defines how to work with this repository. Follow these conventions for consistency and to match Ed's preferences. When in doubt, ask rather than assume.
