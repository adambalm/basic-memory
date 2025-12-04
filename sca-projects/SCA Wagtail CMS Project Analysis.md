---
title: SCA Wagtail CMS Project Analysis
type: analysis
permalink: sca-projects/sca-wagtail-cms-project-analysis
status: canonical
temporal_type: dynamic
valid_from: 2025-11-20
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-11-26
tags:
- sca
- wagtail
- django
- adambalm-server
- remote-analysis
---

# SCA Wagtail CMS Project Analysis

## Project Overview
**Location:** `~/sca` on adambalm server (100.111.114.84)  
**Type:** Django + Wagtail CMS for Springfield Commonwealth Academy  
**Status:** Active development, 3 commits ahead of origin/main  
**Access:** SSH via `ed@100.111.114.84`

## Technology Stack

### Core Framework
- **Django/Wagtail CMS:** Recently upgraded from 6.4.2 → 7.1.1
- **Python:** Backend language
- **PostgreSQL:** Supabase database (port 54322)
- **TailwindCSS:** Frontend styling with Academy Design System
- **Playwright:** Testing framework (v1.55.0)
- **Docker:** Development environment (port 8003)

### Key Integrations
- **Wagtail AI:** Recently added for AI-enhanced content editing
- **Supabase:** Database backend
- **Cloudflare R2:** Media storage (configured)
- **Node.js:** Frontend build tooling

## Project Structure

```
~/sca/
├── springfield_academy/          # Main Django project
│   ├── springfield_academy/     # Core Django apps
│   │   ├── home/                # Homepage app
│   │   ├── programs/            # Academic programs
│   │   ├── news/                # News/blog
│   │   ├── forms/               # Form handling
│   │   ├── navigation/          # Site navigation
│   │   ├── search/              # Search functionality
│   │   ├── standardpages/       # Generic pages
│   │   ├── users/               # User management
│   │   ├── images/              # Custom image handling
│   │   └── utils/               # Shared utilities/blocks
│   ├── templates/               # Wagtail templates
│   ├── static/                  # Static assets
│   ├── static_src/              # TailwindCSS source
│   ├── static_compiled/         # Compiled CSS/JS
│   ├── media/                   # Uploaded media
│   ├── tests/                   # Test files
│   └── manage.py
├── tools/                       # Automation scripts
│   ├── play_crawl.py           # Playwright crawler
│   ├── design_probe.py         # Design analysis
│   ├── image_provider.py       # Image API client
│   └── wagtail_client.py       # Wagtail REST API
├── tasks/                       # Task automation
├── artifacts/                   # Generated artifacts
│   ├── inventory/              # Component inventories
│   └── reports/                # Analysis reports
├── docs/                        # Documentation
├── scripts/                     # Helper scripts
├── backups/                     # Page backups
├── logs/                        # Operation logs
└── screenshots/                 # Visual testing

## Django Apps

### Custom Applications
1. **home** - Homepage with hero, welcome sections
2. **programs** - Academic program listings and details
   - `ProgramCategory` snippets (Elementary, Middle School, etc.)
   - `ProgramLevel` snippets (Beginner, Intermediate, Advanced)
   - `ProgramPage` - Individual program pages
   - `ProgramListingPage` - Filterable program index
3. **news** - News articles and blog posts
4. **forms** - Custom form handling
5. **navigation** - Site navigation management
6. **search** - Search functionality
7. **standardpages** - Generic content pages
8. **users** - User management
9. **images** - Custom image model (`CustomImage`)
10. **utils** - Shared blocks and utilities
    - `StoryBlock` - Rich content blocks
    - `InternalLinkBlock` - Internal linking
    - `CaptionedImageBlock` - Image with captions

## Key Features

### Academy Design System ✅
- TailwindCSS configuration with Academy colors
- Custom button components
- Admissions-focused CTAs
- Responsive mobile navigation
- Modern hero sections

### Content Management
- StreamField architecture for flexible layouts
- Rich text editing (Wagtail 7.x Draftail)
- Image management with custom fields
- Related content linking
- Category and level filtering

### Program Management
- Hierarchical program structure
- Category-based organization
- Level-based filtering
- Featured faculty integration
- Related program suggestions

### Recent Fixes ✅
1. Programs page 404 errors (URL path corruption fixed)
2. Navigation discoverability (Programs link added)
3. Mobile navigation (href attributes fixed)
4. Admin interface issues (rich text parsing fixed)
5. Docker UID/GID permissions resolved

## Development Environment

### Docker Setup (ENFORCED)
- **Container:** `springfield_academy_django`
- **Port:** 8003 (localhost:8003)
- **Admin:** localhost:8003/admin (admin/password)
- **Database:** PostgreSQL via Supabase (172.17.0.1:54322)
- **Safeguards:** Host Django blocked, pre-commit hooks validate

### Port Allocation
- 8003: Django (Docker) ✅ PRIMARY
- 8000: Portainer
- 8001: RAG App
- 8080: Docs site
- 54321-54327: Supabase services

### Commands
```bash
# Start Django
docker compose -f docker-compose.dev.yml up django

# Access admin
http://localhost:8003/admin/

# Load fixtures
make load-data

# Serve docs
bash scripts/serve_docs.sh
```

## Current Development Status

### Git Status
- **Branch:** main (3 commits ahead of origin)
- **Recent commits:**
  1. Wagtail 6.4.2 → 7.1.1 upgrade + wagtail-ai
  2. Pre-upgrade backup
  3. Docker-only compliance validation
  4. Initial project scaffold

### Uncommitted Changes (Many!)
- Modified: Docker compose, MCP config, settings, models, blocks
- Modified: TailwindCSS config, compiled CSS/JS
- Deleted: Test files from docs/
- Untracked: New migrations, templates, scripts, documentation

### Active Development Areas
1. **Design System Parity** - Comparing to sciss.org reference
2. **Component Inventory** - Playwright-based crawling
3. **Image Asset Pipeline** - Unsplash/Pexels integration
4. **Wagtail API Automation** - Programmatic content updates
5. **Visual Testing** - Before/after screenshot comparison

## Implementation Plan (In Progress)

### Completed Phases
- ✅ Infrastructure setup (directories, tools)
- ✅ Playwright crawler for component detection
- ✅ Site branding (Springfield Academy)
- ✅ Academy Design System

### Next Phases
1. **Reference Analysis** - Crawl sciss.org design
2. **Image Pipeline** - Integrate image providers
3. **Wagtail API** - Programmatic content updates
4. **Safe Application** - Backup and apply changes
5. **Verification** - Visual parity checking

## URLs (Working)
- Programs Listing: `/programs/` ✅
- Elementary Mathematics: `/programs/elementary-mathematics/` ✅
- Advanced Literature: `/programs/advanced-literature/` ✅
- Science Fundamentals: `/programs/science-fundamentals/` ✅

## Key Files

### Configuration
- `docker-compose.dev.yml` - Docker orchestration
- `.env.example` - Environment variables template
- `tailwind.config.js` - TailwindCSS configuration
- `.mcp.json` - MCP server configuration

### Documentation
- `CLAUDE.md` - Project context and conventions
- `IMPLEMENTATION_PLAN.md` - Wagtail parity audit plan
- `docs/prd.md` - Product requirements
- `docs/preflight_checklist.md` - Deployment checklist

### Critical Files
- `manage.py` - Django management (wrapped for Docker-only)
- `scripts/docker_only_guard.py` - Enforcement safeguards
- `tools/play_crawl.py` - Component detection crawler

## Notable Patterns

### Test File Organization
All test files MUST go in `/tests/` directory immediately upon creation. Never leave test files in project root.

### Docker-Only Policy
Host Django execution is blocked by:
1. Manage.py wrapper
2. Pre-commit hooks
3. Environment guard script
4. Auto-enforcement tooling

### Wagtail Page Models
- Inherit from `BasePage` (custom)
- Use `StreamField` with `StoryBlock`
- Include search fields
- Provide rich content panels
- Support related content

## AI Features
- Wagtail AI integration for content editing
- OpenAI API key configured
- Rich text AI assistance enabled

## Next Steps
1. Commit uncommitted changes (significant work in progress)
2. Push 3 commits to origin
3. Complete design parity analysis
4. Implement image asset pipeline
5. Automate content updates via Wagtail API

## Notes
- Project based on Wagtail News Template
- Heavy customization for academic use case
- Agent OS workflow integrated
- MCP servers configured (Playwright)
- Active development with many WIP features
- Strong emphasis on automated testing and validation

---

**Analysis Date:** November 20, 2025  
**Analyzed By:** Claude Code via SSH  
**Remote Access:** `ssh ed@100.111.114.84` working ✅
