---
title: Portfolio Site Plan
type: plan
permalink: workspace/planning/portfolio-site-plan
status: draft
temporal_type: dynamic
valid_from: 2025-12-01
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-12-04
tags:
- portfolio
- github-pages
- planning
- draft
- eleventy
- website
---

# Portfolio Site Plan

**Status:** DRAFT - For further revision
**Purpose:** Plan for creating a GitHub Pages portfolio site that serves as a public view into Basic Memory

---

## Vision

Create a GitHub Pages portfolio that serves as a **public view into Ed's Basic Memory knowledge base**. The site is not a copy of content—it's a curated lens that pulls from Basic Memory as the single source of truth.

**Design philosophy:** Simple surface, depth on demand. The sophistication is in the content and connections, not visual complexity.

---

## Architecture Decision

### Basic Memory → GitHub Pages Pipeline

```
basic-memory/           (source of truth - private repo)
       ↓
   build script         (filters, transforms, redacts PII)
       ↓
portfolio-site/         (public repo - GitHub Pages)
       ↓
   ed-oconnell.github.io (or custom domain)
```

**Why this architecture:**
- Content stays in Basic Memory (no duplication)
- Build script handles PII filtering
- Public repo contains only generated output
- Updates flow: edit in BM → run build → push to public

---

## Recommended Stack

### Phase 1: Foundation (4-8 hours)

**Static Site Generator:** Eleventy (11ty)

**Rationale:**
- Zero-JS output by default (fast, accessible)
- Native markdown + frontmatter support (matches Basic Memory)
- Maximum flexibility for future design evolution
- Clean upgrade path to custom themes
- GitHub Actions for automated builds

**Alternative considered:** Quartz (Obsidian-native, graph view) - Save for Phase 2 if graph visualization becomes priority.

### Phase 2: Polish (ongoing)

- Custom typography and color palette
- Graph visualization of protocol connections
- Search functionality
- Mobile optimization

---

## Content Strategy

### What to Publish

| Category | Include | Redact/Exclude |
|----------|---------|----------------|
| **Protocols** | All three (Black Flag, Temporal Validity, Lanesborough) | None - these are the showcase |
| **Architecture Decisions** | Centralized Memory decision with rationale | Specific IP addresses, hostnames |
| **Diagnostics** | "Claude vs ChatGPT" analysis | Session-specific details |
| **Specifications** | Cross-machine context persistence | Internal paths, credentials |
| **Hardware** | General architecture | Specific specs, network config |
| **Professional** | Public resume/bio | Contact details, applications |

### Content Hierarchy

```
Home
├── About (professional narrative)
├── Protocols
│   ├── Black Flag Protocol
│   ├── Temporal Validity Protocol
│   └── Lanesborough Protocol
├── Decisions
│   ├── Centralized Memory Architecture
│   └── [filtered list of canonical decisions]
├── Case Studies
│   ├── Why Claude Failed Where ChatGPT Succeeded
│   └── [filtered diagnostics]
├── Writing (blog/newsletter)
│   ├── [LinkedIn article mirrors]
│   ├── [Original essays]
│   └── [AI collaboration reflections]
└── Colophon (how this site works, meta-reflection)
```

---

## Blog/Newsletter Section

### Content Sources

1. **LinkedIn posts/articles** - Mirror professional content
2. **Original essays** - From `non-fiction/` in Basic Memory
3. **AI collaboration reflections** - Meta-observations on working with AI
4. **Newsletter** - Optional email subscription

### Architecture Options

**Option A: Eleventy + Ghost (Headless)**
- Ghost as headless CMS for blog only
- Eleventy pulls from Ghost API at build time
- Single unified site output
- Newsletter via Ghost's built-in system

**Option B: Ghost for Everything**
- Simpler single platform
- Built-in newsletter, membership, SEO
- Requires Ghost theme customization
- Not GitHub Pages (different hosting)

**Option C: Eleventy with Markdown Blog** (RECOMMENDED START)
- Blog posts as markdown in repo
- LinkedIn articles copied manually
- Newsletter via external service (Buttondown, Substack embed)
- Simplest, most portable
- Can upgrade to Ghost later if newsletter becomes priority

---

## Open Questions

1. **Domain:** Use `ed-oconnell.github.io` or custom domain?
2. **Graph view:** Worth the complexity for Phase 1?
3. **Search:** Essential or nice-to-have?
4. **RSS/Feed:** For updates?
5. **Analytics:** Privacy-respecting option (Plausible, Fathom)?
6. **Ghost status:** What's the current Ghost setup? Self-hosted or Ghost Pro? Worth reviving?
7. **Newsletter priority:** Is email subscription a Phase 1 requirement or later?
8. **LinkedIn sync:** Manual copy or automate extraction?

---

## Success Criteria

- [ ] Site deploys to GitHub Pages
- [ ] Three protocols readable and professional
- [ ] Architecture decision showcases thinking
- [ ] No PII exposed
- [ ] Mobile-friendly
- [ ] Loads in <2 seconds
- [ ] Upgrade path to custom design is clear

---

## Next Steps

1. Dedicated site planning session to resolve open questions
2. Create portfolio repository
3. Set up Eleventy skeleton
4. Create build/sync script
5. Curate initial content
6. Deploy to GitHub Pages
7. Update this plan to canonical when shipped

---

## Relations

- part_of [[Memory System Backlog]]
- extends [[BOOTSTRAP]]
- relates_to [[Architecture Decision - Centralized Memory on adambalm]]