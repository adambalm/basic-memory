---
title: Adambalm Server - Complete System Specifications
type: note
permalink: workspace/hardware/adambalm-server-complete-system-specifications
tags:
- adambalm
- hardware
- system-specs
- gpu
- nvidia
- docker
- ubuntu
- server
---

# Adambalm Server - Complete System Specifications

**Documentation Date:** November 20, 2025  
**Server Hostname:** adambalm  
**Tailscale IP:** 100.111.114.84  
**Local Network IP:** 10.1.11.18/24  
**SSH Access:** `ssh adambalm` (key-based authentication)

---

## 🖥️ Hardware Specifications

### System Overview
**Uptime:** 7 days, 4 hours, 37 minutes  
**Load Average:** 0.21, 0.38, 0.48 (1min, 5min, 15min)  
**Active Users:** 114 sessions  
**Kernel:** Linux 6.8.0-87-generic #88-Ubuntu SMP PREEMPT_DYNAMIC

---

## 💻 Processor

**Model:** Intel Core i5-11400 (11th Generation)  
**Base Clock:** 2.60 GHz  
**Max Turbo:** 4.40 GHz  
**Min Frequency:** 800 MHz  
**Current Scaling:** 21% (power-saving mode)

**Architecture:** x86_64  
**Cores:** 6 physical cores  
**Threads:** 12 logical processors (2 threads per core, Hyper-Threading enabled)  
**Socket:** 1  
**NUMA Nodes:** 1 (node0: CPUs 0-11)

**Performance Characteristics:**
- Excellent for development workloads
- 12 threads support parallel builds
- Turbo boost to 4.4GHz for single-threaded tasks
- Low idle power consumption (800MHz minimum)

---

## 🎮 Graphics Processing Unit (GPU)

### NVIDIA GeForce RTX 5060 Ti

**Driver Version:** 580.95.05  
**CUDA Version:** 13.0  
**Memory:** 16,311 MiB (16 GB GDDR6)  
**Compute Capability:** 12.0 (Ada Lovelace architecture)  
**PCIe Bus ID:** 00000000:01:00.0

**Current Status:**
- Power Draw: 8W / 180W TDP (idle)
- Temperature: 30°C
- Fan Speed: 40%
- GPU Utilization: 6%
- Memory Usage: 0 MiB / 16,311 MiB (0% used)
- No active GPU processes

**Capabilities:**
- ✅ CUDA 13.0 support
- ✅ Machine Learning inference
- ✅ AI model training (local LLMs, stable diffusion)
- ✅ Hardware-accelerated video encoding/decoding
- ✅ Ray tracing (RTX cores)
- ✅ Tensor cores for AI acceleration
- ✅ 16GB VRAM suitable for:
  - Large language models (7B-13B parameters)
  - Stable Diffusion XL
  - Video processing workflows
  - Multi-model inference

**Persistence Mode:** OFF  
**ECC Memory:** Not Available (consumer GPU)  
**Display Active:** OFF (headless server)

---

## 🧠 Memory

**Total Physical RAM:** 64 GB (65,606,900 kB)  
**Available RAM:** 58 GB (58,350,488 kB)  
**Currently Free:** 49 GB (49,650,968 kB)  
**Used:** ~7 GB  
**Buffers/Cache:** ~9 GB  

**Swap:**
- Total: 8 GB (8,388,604 kB)
- Used: 0 GB
- Free: 8 GB (100% available)

**Memory Utilization:** ~11% (very light load)  
**Swap Usage:** 0% (no memory pressure)

**Capacity Assessment:**
- Excellent for development workloads
- Can run multiple Docker containers simultaneously
- Sufficient for large builds and test suites
- Supports memory-intensive applications (databases, caching)

---

## 💾 Storage Configuration

### Disk Layout

#### NVMe Drive 1 (Primary)
**Device:** /dev/nvme0n1  
**Capacity:** 931.5 GB (1 TB NVMe SSD)  
**Partitioning:**
- `/dev/nvme0n1p1` - 1 GB (EFI System Partition, 1% used)
- `/dev/nvme0n1p2` - 2 GB (Boot partition, 16% used, 286 MB)
- `/dev/nvme0n1p3` - 928.5 GB (LVM physical volume)

#### NVMe Drive 2 (Secondary)
**Device:** /dev/nvme1n1  
**Capacity:** 931.5 GB (1 TB NVMe SSD)  
**Status:** Available (not currently mounted)

### LVM Configuration
**Volume Group:** ubuntu-vg  
**Logical Volume:** ubuntu-lv  
**LV Size:** 1.82 TiB (spans both drives)  
**Filesystem:** ext4  
**Mount Point:** `/`

### Filesystem Usage
**Root (/):** 1.8 TB total, 164 GB used, 1.6 TB available (10% used)  
**Boot (/boot):** 2.0 GB total, 286 MB used, 1.6 GB available (16% used)  
**EFI (/boot/efi):** 1.1 GB total, 6.2 MB used, 1.1 GB available (1% used)

**Storage Summary:**
- ✅ 1.6 TB free space available
- ✅ Two high-speed NVMe SSDs (excellent I/O performance)
- ✅ LVM provides flexibility for expansion/snapshots
- ✅ Plenty of space for development projects, Docker images, databases

---

## 🌐 Network Configuration

### Network Interfaces

#### Loopback (lo)
**IPv4:** 127.0.0.1/8

#### Ethernet (eno1)
**Type:** Gigabit Ethernet  
**MAC:** 04:42:1a:96:ce:54  
**IPv4:** 10.1.11.18/24 (DHCP, local network)

#### Tailscale VPN (tailscale0)
**Type:** WireGuard VPN tunnel  
**MAC:** 8e:a4:0e:fb:2c:43  
**IPv4:** 100.111.114.84/32 (Tailscale mesh network)  
**Status:** Active, connected to tailnet

#### Docker Networks
**docker0:** 172.17.0.1/16 (default bridge)  
**br-5aac6946330f:** 172.19.0.1/16 (custom bridge)  
**br-d265582a68ff:** 172.18.0.1/16 (custom bridge)

**Multiple veth interfaces** for container networking (10+ active)

### Network Capabilities
- ✅ Gigabit local network (10.1.11.x)
- ✅ Tailscale mesh VPN (secure remote access)
- ✅ Multiple Docker networks for service isolation
- ✅ SSH server active (port 22)
- ✅ SSH key-based authentication configured

---

## 🐧 Operating System

**Distribution:** Ubuntu 24.04.3 LTS (Noble Numbat)  
**Codename:** noble  
**Version ID:** 24.04  
**Base:** Debian  
**Kernel:** 6.8.0-87-generic  
**Architecture:** x86_64  
**Build Type:** SMP PREEMPT_DYNAMIC (optimized for desktop/server hybrid)

**Support:**
- LTS Release (Long Term Support until 2029)
- Regular security updates
- Stable, well-documented platform

---

## 🛠️ Development Environment

### Programming Languages

#### Python
**Version:** 3.12.3  
**Package Manager:** pip 24.0  
**Location:** /usr/lib/python3/dist-packages/pip  
**Status:** System Python installation

### Version Control
**Git:** 2.43.0

### AI Development Tools
**Claude Code:** v2.0.19  
**Location:** `/home/ed/.cursor-server/extensions/anthropic.claude-code-2.0.19-linux-x64/`  
**Binary Path:** `/home/ed/.cursor-server/extensions/anthropic.claude-code-2.0.19-linux-x64/resources/native-binary/claude`  
**Status:** Installed via Cursor extension

---

## 🐳 Docker Infrastructure

### Docker Engine
**Version:** 28.5.1 (build e180ab8)  
**Docker Compose:** v2.40.3  
**Status:** Active and running (docker.service)

### Running Containers (14 active)

#### Application Containers

**1. Portainer** (Container Management)
- Image: `portainer/portainer-ce:latest`
- Status: Up 7 days
- Ports: 8000 (HTTP), 9443 (HTTPS)
- Purpose: Docker management UI

**2. Open WebUI** (LLM Interface)
- Image: `ghcr.io/open-webui/open-webui:main`
- Status: Up 7 days (healthy)
- Port: 3000 (maps to container 8080)
- Purpose: Web interface for local LLM interaction

**3. Springfield Academy Django** (SCA Website)
- Image: `sca-django` (custom)
- Container: `springfield_academy_django`
- Status: Up 7 days
- Ports: 8003 → 8000
- Purpose: Wagtail CMS for Springfield Commonwealth Academy

#### Supabase Stack (11 containers)

**Database & Core Services:**

**4. PostgreSQL Database** (`supabase_db_sca`)
- Image: `supabase/postgres:17.6.1.002`
- Status: Up 7 days (healthy)
- Port: 54322 → 5432
- Purpose: Main PostgreSQL database with Supabase extensions

**5. Kong API Gateway** (`supabase_kong_sca`)
- Image: `supabase/kong:2.8.1`
- Status: Up 7 days (healthy)
- Port: 54321 → 8000
- Purpose: API gateway and request routing

**6. GoTrue Auth** (`supabase_auth_sca`)
- Image: `supabase/gotrue:v2.179.0`
- Status: Up 7 days (healthy)
- Purpose: Authentication service

**7. Realtime Server** (`supabase_realtime_sca`)
- Image: `supabase/realtime:v2.47.0`
- Status: Up 7 days (healthy)
- Purpose: WebSocket real-time subscriptions

**8. PostgREST API** (`supabase_rest_sca`)
- Image: `supabase/postgrest:v13.0.6`
- Status: Up 7 days
- Purpose: Automatic REST API generation from database

**9. Storage API** (`supabase_storage_sca`)
- Image: `supabase/storage-api:v1.26.5`
- Status: Up 7 days (healthy)
- Purpose: Object storage and file uploads

**10. Studio (Admin UI)** (`supabase_studio_sca`)
- Image: `supabase/studio:2025.09.08`
- Status: Up 7 days (healthy)
- Port: 54323 → 3000
- Purpose: Database management and admin interface

**11. Postgres Meta** (`supabase_pg_meta_sca`)
- Image: `supabase/postgres-meta:v0.91.6`
- Status: Up 7 days (healthy)
- Purpose: PostgreSQL metadata API

**12. Mail Pit** (`supabase_inbucket_sca`)
- Image: `supabase/mailpit:v1.22.3`
- Status: Up 7 days (healthy)
- Port: 54324 → 8025
- Purpose: Email testing and SMTP server

**13. Vector Logging** (`supabase_vector_sca`)
- Image: `supabase/vector:0.28.1-alpine`
- Status: Up 7 days (healthy)
- Purpose: Log aggregation and processing

**14. Analytics** (`supabase_analytics_sca`)
- Image: `supabase/logflare:1.18.4`
- Status: Up 7 days (healthy)
- Port: 54327 → 4000
- Purpose: Analytics and logging dashboard

### Docker Network Summary
- All containers healthy (no crashed services)
- 7 days uptime (stable, reliable)
- Multiple isolated networks for security
- Ports mapped to host for external access

---

## 🚀 Active Services

### System Services (systemd)

**Docker Engine** (`docker.service`)
- Status: Active/Running
- Purpose: Container orchestration

**SSH Server** (`ssh.service`)
- Status: Active/Running
- Purpose: Secure remote access
- Key-based auth configured for user 'ed'

**Tailscale** (`tailscaled.service`)
- Status: Active/Running
- Purpose: Mesh VPN connectivity
- IP: 100.111.114.84

---

## 📂 Active Projects

Located in `/home/ed/`:

1. **sca** - Springfield Academy Wagtail CMS (Django + Wagtail 7.1.1)
2. **scglobal** - Empty directory (potential future project)
3. **sfca** - Project with git repo and Claude config
4. **contentful-marketo-ai-bridge** - Large backend project with Agent OS
5. **ghost-writer** - Large project (19MB+) with Agent OS
6. **playwright-mcp** - Playwright automation scripts
7. **mcp-audit** - MCP server auditing tools
8. **portfolio** - Portfolio site
9. **metaops** / **meta-ops-validator** - Meta operations tools
10. **ml-roadmap** - Machine learning project planning
11. **context-integrity** - Context validation tools
12. **html-preview** - HTML preview utilities
13. **starting-ragchatbot-codebase** - RAG chatbot starter
14. **storage-audit** - Storage auditing tools
15. **agent-os-adaptive** - Adaptive Agent OS implementation
16. **test-claude** - Claude testing environment

**Plus:** Various utility directories, configuration files, and development tools

---

## 🔒 Security Configuration

### Authentication
- ✅ SSH key-based authentication (ED25519)
- ✅ Password authentication disabled for keys
- ✅ Tailscale VPN for secure remote access
- ✅ Docker container isolation

### Network Security
- ✅ Private network (10.1.11.x) + VPN overlay
- ✅ Firewall-managed port exposure
- ✅ Container network isolation
- ✅ No public IP exposure (behind Tailscale)

---

## 📊 Performance Characteristics

### Current Load
- **CPU Load:** Light (0.21, 0.38, 0.48)
- **Memory Usage:** 11% (7GB / 64GB)
- **Swap Usage:** 0% (no memory pressure)
- **GPU Utilization:** 6% (idle)
- **Disk Usage:** 10% (164GB / 1.8TB)

### Capacity Assessment
**Workload Suitability:**
- ✅ **Excellent** for web development (plenty of headroom)
- ✅ **Excellent** for Docker-based services (14 containers at 11% RAM)
- ✅ **Excellent** for local LLM inference (RTX 5060 Ti 16GB)
- ✅ **Excellent** for build/test pipelines (12 cores)
- ✅ **Excellent** for database hosting (64GB RAM + NVMe)
- ✅ **Good** for AI/ML training (16GB VRAM, CUDA 13.0)

**Scaling Potential:**
- Can easily handle 5-10x more Docker containers
- Can run multiple LLMs simultaneously
- Sufficient for large-scale development projects
- No current bottlenecks

---

## 🎯 Use Cases & Capabilities

### Current Active Workloads
1. **Web Development** - Springfield Academy CMS
2. **Database Services** - Supabase full stack
3. **Container Management** - Portainer
4. **LLM Interface** - Open WebUI for local AI models
5. **Development Tools** - Claude Code, Git, Python

### Potential Future Workloads
- ✅ Machine Learning model training (16GB VRAM)
- ✅ Video processing/transcoding (GPU acceleration)
- ✅ Multiple concurrent development environments
- ✅ Large-scale database operations
- ✅ CI/CD build pipelines
- ✅ Local AI model serving (Ollama, LLaMA, etc.)

---

## 💡 Key Strengths

1. **Powerful CPU** - 11th Gen i5 with 12 threads for parallel workloads
2. **Massive RAM** - 64GB enables heavy multitasking without memory pressure
3. **Modern GPU** - RTX 5060 Ti 16GB perfect for local AI/ML development
4. **Fast Storage** - Dual NVMe SSDs with 1.6TB free space
5. **Stable Platform** - Ubuntu 24.04 LTS with 7+ days uptime
6. **Comprehensive Stack** - Docker, Python, Git, Claude Code all configured
7. **Secure Access** - Tailscale VPN + SSH keys for reliable remote work
8. **CUDA Support** - Latest CUDA 13.0 for GPU-accelerated workloads

---

## 📝 Notes

### System Stability
- 7 days uptime with no crashes
- All 14 Docker containers healthy
- Low system load indicates plenty of headroom
- No swap usage (excellent memory management)

### GPU Readiness
- CUDA 13.0 available for AI/ML workloads
- 16GB VRAM suitable for:
  - Local LLM inference (LLaMA 2 13B, Mistral, etc.)
  - Stable Diffusion XL image generation
  - Fine-tuning smaller models
  - Multi-model serving

### Development Environment
- Claude Code installed and functional
- SSH key authentication configured
- Multiple active projects ready for work
- Docker ecosystem fully operational

### Networking
- Tailscale provides secure, reliable remote access
- Multiple Docker networks for service isolation
- SSH access from suphouse (Windows) working perfectly

---

**System Specifications Captured:** November 20, 2025 02:41 UTC  
**Captured By:** Claude Code (Sonnet 4.5) via SSH  
**Method:** Direct SSH commands from suphouse to adambalm  
**Next Review:** As needed for capacity planning or upgrades

---

**This is a high-performance development server well-suited for:**
- Multi-project development workflows
- Container-based microservices
- Local AI/ML experimentation
- Large-scale database operations
- Build and test automation
- Remote collaboration via Tailscale VPN
