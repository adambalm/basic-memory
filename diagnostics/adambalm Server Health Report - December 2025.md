---
title: adambalm Server Health Report - December 2025
type: diagnostic
permalink: diagnostics/adambalm-server-health-report-december-2025
status: canonical
temporal_type: point-in-time
valid_from: 2025-12-04
valid_until: null
supersedes: null
superseded_by: null
last_verified: 2025-12-04
tags:
- adambalm
- infrastructure
- health-check
- diagnostic
- december-2025
---

# adambalm Server Health Report - December 2025

## Executive Summary

**Overall Health: EXCELLENT** ✅

adambalm is a well-provisioned Ubuntu 24.04 server running a comprehensive AI/development stack. The system has abundant resources (62GB RAM, 1.8TB disk, RTX 5060 Ti GPU), stable uptime (5+ days), and no critical issues. The only failed service (openipmi) is non-essential.

---

## 1. System Vital Signs

| Metric | Value | Assessment |
|--------|-------|------------|
| **OS** | Ubuntu 24.04.3 LTS | Current LTS ✅ |
| **Kernel** | 6.8.0-88-generic | Recent ✅ |
| **Uptime** | 5 days, 19 hours | Stable ✅ |
| **Load Average** | 0.92, 0.45, 0.27 | Low ✅ |
| **RAM** | 4.5GB used / 62GB total (7%) | Excellent ✅ |
| **Swap** | 0B used / 8GB total | Unused ✅ |
| **Disk** | 164GB used / 1.8TB (10%) | Excellent ✅ |
| **GPU** | RTX 5060 Ti, 0/16GB VRAM, 6% util | Idle ✅ |

### Network
- **Primary IP:** 10.1.11.18/24 (eno1)
- **Tailscale IP:** 100.111.114.84/32
- **Docker bridges:** 172.17.0.0/16, 172.18.0.0/16, 172.19.0.0/16

---

## 2. Running Services

### Core Services (Active)
| Service | Status | Purpose |
|---------|--------|---------|
| Docker | ✅ Active | Container orchestration |
| Ollama | ✅ Active | Local LLM inference |
| Samba | ✅ Active | File sharing (Dan G access?) |
| Tailscaled | ✅ Active | VPN mesh networking |
| SSH | ✅ Active | Remote access |

### Not Running (By Design)
| Service | Status | Notes |
|---------|--------|-------|
| Caddy | Inactive | Configured but disabled |
| Nginx | Not installed | - |
| Apache | Not installed | - |

### Basic Memory MCP
```
Running via: uvx basic-memory mcp --transport streamable-http --port 8765 --host 0.0.0.0
Process IDs: 599489, 599512
Transport: streamable-http (accessible over network)
```

---

## 3. Installed Infrastructure

### Docker Containers (14 running)

**AI/Development:**
| Container | Status | Port | Purpose |
|-----------|--------|------|---------|
| open-webui | Healthy | 3000→8080 | LLM web interface |
| portainer | Up | 9443, 8000 | Docker management |

**SCA Application Stack:**
| Container | Status | Port | Purpose |
|-----------|--------|------|---------|
| springfield_academy_django | Up | 8003→8000 | SCA Django app |
| supabase_studio_sca | Healthy | 54323→3000 | Database UI |
| supabase_kong_sca | Healthy | 54321→8000 | API Gateway |
| supabase_db_sca | Healthy | 54322→5432 | PostgreSQL |
| supabase_auth_sca | Healthy | 9999 | Authentication |
| supabase_rest_sca | Up | 3000 | REST API |
| supabase_realtime_sca | Healthy | 4000 | WebSockets |
| supabase_storage_sca | Healthy | 5000 | File storage |
| supabase_pg_meta_sca | Healthy | 8080 | Postgres metadata |
| supabase_analytics_sca | Healthy | 54327→4000 | Analytics |
| supabase_vector_sca | Healthy | - | Vector embeddings |
| supabase_inbucket_sca | Healthy | 54324→8025 | Email testing |

### Ollama Models (52.4GB total)
| Model | Size | Purpose |
|-------|------|---------|
| qwq:latest | 19GB | Advanced reasoning |
| qwen2.5vl:7b | 6.0GB | Vision-language |
| qwen3:latest | 5.2GB | General |
| deepseek-r1:latest | 5.2GB | Reasoning |
| qwen2.5-coder:latest | 4.7GB | Code generation |
| llama3:latest | 4.7GB | General |
| gemma3:latest | 3.3GB | General |
| qwen:latest | 2.3GB | General |
| llama3.2:latest | 2.0GB | Compact |

### Docker Disk Usage
| Type | Total | Active | Reclaimable |
|------|-------|--------|-------------|
| Images | 52.75GB | 17 | 41.56GB (78%) |
| Containers | 1.529GB | 14 | 302.4MB |
| Volumes | 4.489GB | 5 | 177MB |

---

## 4. Failed/Problematic State

### Failed Services
| Service | Status | Impact | Action |
|---------|--------|--------|--------|
| openipmi.service | Failed | None - IPMI not used | Can disable |

### Recent Errors (24h)
**None found** - journalctl shows no errors in the past 24 hours.

---

## 5. Evidence of Past Trauma

### Directory Archaeology
| Directory | Size | Observation |
|-----------|------|-------------|
| ghost-writer | 7.8GB | Caddy config references this |
| ml-roadmap | 7.0GB | Large ML project |
| meta-ops-validator | 709MB | - |
| sca | 638MB | SCA-related content |
| contentful-marketo-ai-bridge | 411MB | Marketing integration |
| starting-ragchatbot-codebase | 218MB | RAG chatbot project |
| basic-memory | 1.4MB | Memory system |
| agent-os-adaptive | 2.1MB | Agent OS variant |

### Caddy Configuration (Inactive but Present)
```caddy
https://adambalm.tail069d40.ts.net {
    tls internal
    root * /home/ed/ghost-writer
    # iOS certificate distribution
    # Proxies to ports 5001, 8001
}
```
**Observation:** Ghost-writer project was configured for internal TLS on Tailscale domain, but Caddy is now disabled.

---

## 6. TLS State

### Certificate Status
| Source | Status | Notes |
|--------|--------|-------|
| Let's Encrypt | ❌ Not installed | No certbot |
| Caddy Auto-TLS | ❌ Inactive | Service disabled |
| Caddy Internal TLS | Configured | Would use `tls internal` |

### Current TLS Exposure
- **Tailscale:** Provides encrypted tunnel to 100.111.114.84
- **Local network:** Services on 10.1.11.18 are unencrypted
- **Docker:** Internal container communication is unencrypted (normal)

### Recommendation
Tailscale provides adequate encryption for remote access. Internal services don't need TLS unless exposed to internet.

---

## 7. Policies/Constraints

### No User Cron Jobs
```
No crontab for ed
```

### Systemd Timers (Standard Ubuntu)
- apt-daily.timer
- apt-daily-upgrade.timer
- fstrim.timer
- snapd.refresh.timer
- logrotate.timer

### Network Policies
- Samba running (implies file sharing configured)
- No firewall rules examined (would need sudo)

---

## 8. Health Assessment

### Strengths ✅
1. **Abundant resources** - 62GB RAM, RTX 5060 Ti, 1.8TB disk
2. **Clean error logs** - No errors in past 24 hours
3. **Healthy containers** - All 14 Docker containers healthy
4. **Modern stack** - Ubuntu 24.04 LTS, recent kernel
5. **Proper networking** - Tailscale for secure remote access
6. **GPU available** - RTX 5060 Ti for ML inference

### Areas of Note ⚠️
1. **Caddy disabled** - Was configured for ghost-writer but inactive
2. **openipmi failed** - Non-critical, can be disabled
3. **Docker image bloat** - 41.56GB reclaimable
4. **Samba running** - Verify this is intentional

### No Issues ✅
- Disk space: 90% free
- Memory: 93% free
- Load: Very low
- All critical services running

---

## 9. Questions for Dan G

1. **Samba:** Is the Samba share intentionally active? Who uses it?
2. **Ghost-writer:** What was this project? Is Caddy supposed to be running?
3. **openipmi:** Can we disable this service since IPMI isn't used?
4. **Docker cleanup:** Safe to run `docker system prune` to reclaim 41GB?
5. **Network exposure:** Are any services meant to be accessible from LAN (10.1.11.x)?
6. **Backups:** Is there a backup strategy for this server?
7. **Supabase SCA:** Is the full Supabase stack still needed for SCA development?

---

## 10. Recommendations

### Immediate (Low Risk)
1. **Disable openipmi:**
   ```bash
   sudo systemctl disable openipmi.service
   sudo systemctl mask openipmi.service
   ```

2. **Reclaim Docker disk space:**
   ```bash
   docker image prune -f  # Remove dangling images
   # Full prune only after confirming unused: docker system prune -a
   ```

### Short-term
3. **Document Caddy intent:** Decide if ghost-writer should be served
4. **Review Samba shares:** Ensure only intended directories are exposed
5. **Basic Memory systemd:** Consider converting to systemd service for reliability

### Long-term
6. **Backup strategy:** Implement automated backups for /home/ed
7. **Monitoring:** Consider Prometheus/Grafana for resource monitoring
8. **GPU utilization:** Ollama has access to 16GB VRAM - could run larger models

---

## Relations

- documents [[Architecture Decision - Centralized Memory on adambalm]]
- part_of [[Memory Architecture Evolution - Decision Tracking]]
- informs [[Pending Decision - Sync Automation]]
