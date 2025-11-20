---
title: Suphouse (Asus Vivobook) - Complete System Specifications
type: note
permalink: workspace/hardware/suphouse-asus-vivobook-complete-system-specifications
tags:
- suphouse
- hardware
- system-specs
- laptop
- asus
- vivobook
- windows-11
- development
---

# Suphouse (Asus Vivobook) - Complete System Specifications

**Documentation Date:** November 20, 2025  
**Hostname:** SUPHOUSE  
**Local IP:** 192.168.1.22  
**Tailscale IP:** 100.126.163.59  
**Owner:** angelene2000@yahoo.com  
**Primary User:** Guest1 (Administrator)

---

## 🖥️ Hardware Specifications

### System Information
**Manufacturer:** ASUSTeK COMPUTER INC.  
**Model:** Vivobook_ASUSLaptop X1502ZA_F1502ZA  
**System Type:** x64-based PC (Laptop)  
**BIOS:** American Megatrends International, LLC. X1502ZA.312 (3/1/2023)  
**Purchase Date:** March 14, 2025  
**Form Factor:** 15.6" Ultrabook

---

## 💻 Processor

**Model:** Intel Core i7-1255U (12th Generation Alder Lake)  
**Architecture:** x86_64  
**Base Clock:** 1.7 GHz  
**Max Turbo:** 4.7 GHz (estimated for 1255U)  
**Cores:** 10 cores total
- 2 Performance cores (P-cores)
- 8 Efficient cores (E-cores)

**Threads:** 12 logical processors (2P+8E cores with Hyper-Threading on P-cores)  
**Cache:** 12 MB Intel Smart Cache  
**TDP:** 15W (configurable up to 55W)  
**Intel Features:**
- Intel Turbo Boost Technology
- Intel Hyper-Threading
- Intel vPro support
- Hardware-accelerated virtualization (VT-x)

**Performance Characteristics:**
- Excellent for mobile development workflows
- Hybrid architecture optimizes battery life
- P-cores handle demanding tasks
- E-cores handle background processes efficiently

---

## 🧠 Memory (RAM)

**Total Capacity:** 16 GB (16,078 MB)  
**Configuration:** 2x 8GB modules (dual-channel)  
**Manufacturer:** Samsung  
**Speed:** 3200 MHz (DDR4-3200)  
**Type:** DDR4 SDRAM  
**Form Factor:** SO-DIMM (laptop)

**Current Usage (as of Nov 20, 2025):**
- Total: 16 GB
- Used: ~13.4 GB (83%)
- Available: 2.9 GB (18%)
- Virtual Memory Max: 37.6 GB
- Virtual Memory In Use: 23.8 GB (63%)

**Memory Assessment:**
- System under moderate load
- Virtual memory being utilized
- Adequate for typical development tasks
- May benefit from closing unused applications

---

## 💾 Storage

### NVMe SSD
**Model:** Intel SSDPEKNU512GZ  
**Capacity:** 512 GB (512,105,932,800 bytes)  
**Interface:** NVMe PCIe (SCSI)  
**Media Type:** Fixed hard disk (SSD)  
**Form Factor:** M.2 2280

### Logical Drives

**C: Drive (System)**
- **Total Size:** 475 GB (510,526,820,352 bytes)
- **Used:** 149 GB
- **Free:** 325 GB (349,260,775,424 bytes)
- **Usage:** 31%
- **Filesystem:** NTFS

**Storage Performance:**
- NVMe provides excellent read/write speeds
- Fast boot times and application loading
- Sufficient free space for development work
- 325GB available for projects and tools

---

## 🎮 Graphics

### Integrated GPU
**Model:** Intel Iris Xe Graphics  
**Type:** Integrated (shares system RAM)  
**Memory:** 1 GB dedicated (dynamically allocated from system RAM)  
**Driver Version:** 31.0.101.4255  
**Architecture:** Intel Xe (12th Gen)  
**DirectX Support:** DirectX 12  
**Compute Units:** 96 EUs (Execution Units)

**Capabilities:**
- ✅ 4K video playback
- ✅ Hardware video encoding/decoding
- ✅ Multiple display support
- ✅ Basic OpenGL/Vulkan support
- ⚠️ Limited for GPU-intensive tasks (no dedicated GPU)
- ⚠️ Not suitable for AI/ML training (compared to dedicated GPUs)

**Note:** For GPU-intensive tasks, use adambalm server (RTX 5060 Ti 16GB)

### Additional Display Device
**Model:** Epson Projection Idd Device  
**Driver:** 9.40.11.700  
**Purpose:** Projector/external display support

---

## 🐧 Operating System

**OS:** Microsoft Windows 11 Home  
**Version:** 10.0.26100 Build 26100  
**Architecture:** 64-bit  
**Build Type:** Multiprocessor Free  
**Configuration:** Standalone Workstation  
**Product ID:** 00342-22183-84885-AAOEM  
**Install Date:** March 14, 2025

**System Directories:**
- **Windows:** C:\WINDOWS
- **System32:** C:\WINDOWS\system32
- **Boot Device:** \Device\HarddiskVolume1

**Regional Settings:**
- **Locale:** en-us (English, United States)
- **Time Zone:** (UTC-05:00) Eastern Time (US & Canada)
- **Input Method:** English (United States)

**Windows Updates:**
4 Hotfixes Installed:
- KB5066131
- KB5068861
- KB5067360
- KB5067035

**System Status:**
- **Uptime:** 9 days, 14 hours (stable)
- **Last Boot:** November 10, 2025, 12:55:09 PM

---

## 🌐 Network Configuration

### Network Interfaces

#### 1. Wi-Fi (Primary Connection)
**Adapter:** Intel Wi-Fi 6 AX201 160MHz  
**Status:** Connected  
**DHCP:** Enabled  
**DNS Suffix:** lan

**IPv4:**
- Address: 192.168.1.22
- Subnet: 255.255.255.0
- Gateway: 192.168.1.1

**IPv6 Addresses:**
- 2600:6c65:6540:7015::1020
- 2600:6c65:65f0:82b0::1020
- 2600:6c65:65f0:82b0:16c9:a551:2c7b:81c3
- fd00:b0bb:e521:78b8::1020 (ULA)
- fd00:b0bb:e521:78b8:311:49c5:c86e:ec46 (ULA)
- Temporary: 2600:6c65:65f0:82b0:c513:9726:bd36:4025
- Link-local: fe80::3e02:9ddf:7a27:53c4%5

**Capabilities:**
- Wi-Fi 6 (802.11ax)
- 160 MHz channel width
- Dual-band (2.4 GHz / 5 GHz)
- Excellent modern wireless performance

#### 2. Tailscale VPN (tailscale0)
**Type:** Wintun Userspace Tunnel  
**Status:** Connected  
**DNS Suffix:** tail069d40.ts.net

**IPv4:** 100.126.163.59/32  
**IPv6:**
- fd7a:115c:a1e0::4901:a33b
- fe80::6bcb:85f0:ed6d:e8b4%7 (link-local)

**Tailnet Peers:**
- adambalm (100.111.114.84) - Linux server ✅ ACTIVE
- alexispc (100.99.93.127) - Offline 40 days
- daniel-macbook-pro (100.79.185.8) - Offline 105 days
- eds-imac (100.96.95.89) - Offline 12 minutes
- iphone-13 (100.64.31.8) - Offline 21 days
- iphone173 (100.93.129.49) - Active
- tattoonows-mac-pro (100.91.110.24) - Active

**SSH to adambalm:** `ssh adambalm` (key-based auth configured ✅)

#### 3. Bluetooth Network Connection
**Status:** Media disconnected  
**Type:** Personal Area Network (PAN)

#### 4. Wireless LAN Adapters (Virtual)
**Local Area Connection* 1:** Media disconnected  
**Local Area Connection* 2:** Media disconnected

### Network Features
- ✅ Gigabit-capable Wi-Fi 6
- ✅ Tailscale mesh VPN for secure remote access
- ✅ IPv4 and IPv6 dual-stack
- ✅ SSH configured for remote server access
- ✅ Multiple network adapters for flexibility

---

## 🛠️ Development Environment

### Programming Languages

**Python**
- **Version:** 3.12.10
- **Package Manager:** pip (included)
- **Location:** System-wide installation

**Node.js**
- **Version:** 20.18.1 (LTS)
- **npm:** 11.6.2
- **Package Manager:** npm (global)

### Version Control
**Git:** 2.47.1.windows.1 (latest for Windows)

### Code Editors

**Visual Studio Code**
- **Location:** C:\Users\Guest1\AppData\Local\Programs\Microsoft VS Code\
- **Binary:** code.cmd
- **Extensions:** Claude Code integration available

**Cursor IDE**
- **Location:** C:\Program Files\cursor\
- **Binary:** cursor.cmd
- **AI Features:** Built-in AI assistance

### Testing & Automation

**Playwright**
- **Version:** 1.56.1 (pinned via .npmrc)
- **Browser Binaries:** C:/Users/Guest1/AppData/Local/ms-playwright/
- **Purpose:** Browser automation and testing

### AI Development Tools

**Claude Code**
- **Version:** 2.0.47 (latest as of Nov 20, 2025)
- **Install Method:** Global npm installation
- **Startups:** 47 sessions
- **Theme:** light-daltonized
- **Auto Updates:** Enabled
- **User ID:** 5dd51c56049a85f9f88636eed3f6aa05e501acb111bd223c8964cf202c294c23

**Claude Code Features Enabled:**
- Task tracking (todos)
- Plan mode
- Terminal integration
- Memory command
- Custom commands
- Permissions system
- Web tasks
- Thinking mode (tab toggle)

**MCP Servers (User-Level):**
Configured in `~/.claude.json`:
- Playwright MCP (@playwright/mcp)
- Context7 MCP (@upstash/context7-mcp)
- Basic Memory MCP (@basicmachines-co/basic-memory)
- GitHub MCP (built-in)

**Basic Memory:**
- **Directory:** C:/Users/Guest1/.claude-memory/
- **Project:** main
- **Status:** Active
- **Notes:** Multiple system specs, SSH configs, project analyses

---

## 📁 Project Structure

**ClaudeProjects Root:** `C:/Users/Guest1/ClaudeProjects/`

**Active Projects:**
1. **SCA Projects/** - Monorepo for Springfield Commonwealth Academy
   - TennisFlyer (shipped)
   - ResumeFactory (active)
   - c2s_fire_drill (test directory)
   
2. **AutonomousAdmissionsAgent/** - Agent OS test installation

3. **.claude/** - User-level Claude Code configuration
   - Global settings
   - Personal skills
   - Cross-project patterns

4. **.archive/** - Archived projects

5. **_scratch/** - Temporary working directory

**Configuration Files:**
- `CLAUDE.md` - Workspace conventions
- `.mcp.json` - Workspace MCP configuration (when needed)

**Development Paths:**
- Projects: `C:/Users/Guest1/ClaudeProjects/`
- Playwright: `C:/Users/Guest1/AppData/Local/ms-playwright/`
- Basic Memory: `C:/Users/Guest1/.claude-memory/`
- SSH Keys: `C:/Users/Guest1/.ssh/`

---

## 🔒 Security Features

### Virtualization-Based Security (VBS)
**Status:** Running ✅

**Enabled Security Properties:**
- Base Virtualization Support
- Secure Boot
- DMA Protection
- UEFI Code Readonly
- Mode Based Execution Control
- APIC Virtualization

**Services:**
- Hypervisor enforced Code Integrity (configured & running)
- App Control Policy: Enforced (user mode: Off)

### Hyper-V
**Status:** Hypervisor detected  
**Note:** Full Hyper-V features not displayed due to VBS

### Authentication
- ✅ SSH key-based authentication (ED25519)
- ✅ Tailscale VPN encryption
- ✅ Administrator privileges for Guest1
- ✅ Windows Hello capable (hardware)

### Network Security
- ✅ Private network (192.168.1.x) + VPN
- ✅ Tailscale mesh encryption
- ✅ Wi-Fi 6 WPA3 capable
- ✅ No public IP exposure

---

## 🔋 Power Status

**Battery:**
- **Status:** Charging (AC Power)
- **Current Charge:** 18%
- **Battery Health:** Normal operation

**Power Profile:**
- Laptop optimized for balanced performance
- Intel 12th Gen hybrid architecture manages power efficiently
- Wi-Fi 6 power management enabled

**Note:** System typically runs on AC power during development work

---

## 📊 Performance Status

### Current System Load (Nov 20, 2025 03:00 AM)

**CPU:**
- Current Clock: 1.7 GHz (base, power-saving)
- Turbo Available: Up to 4.7 GHz
- 12 threads available for parallel tasks

**Memory:**
- Used: 13.4 GB / 16 GB (83%)
- Available: 2.9 GB (18%)
- Virtual Memory: 23.8 GB / 37.6 GB (63%)
- Assessment: Moderate load, consider closing unused apps

**Storage:**
- C: Drive: 31% used (325 GB free)
- NVMe performance: Excellent
- No storage pressure

**Network:**
- Wi-Fi: Connected and stable
- Tailscale: Active connection to tailnet
- Remote server (adambalm): Accessible via SSH

**Uptime:** 9 days, 14 hours (stable operation)

---

## 🎯 Use Cases & Capabilities

### Current Workloads
1. **Local Development**
   - Node.js web applications
   - Python scripting and automation
   - Git version control workflows
   - Code editing (VS Code, Cursor)

2. **Browser Automation**
   - Playwright testing
   - Visual regression testing
   - E2E test development

3. **AI-Assisted Development**
   - Claude Code sessions (47 startups)
   - MCP server integrations
   - Basic Memory for continuity
   - Remote code analysis via SSH

4. **Project Management**
   - Monorepo development (SCA Projects)
   - Multiple concurrent projects
   - Document generation (resumes, flyers)

### Strengths
✅ **Portable:** Laptop form factor for mobility  
✅ **Modern CPU:** 12th Gen i7 with hybrid architecture  
✅ **Fast Storage:** NVMe SSD for quick builds  
✅ **Excellent Connectivity:** Wi-Fi 6 + Tailscale VPN  
✅ **Development Ready:** All tools pre-configured  
✅ **Secure:** VBS, SSH keys, VPN encryption  
✅ **Integrated Ecosystem:** Works seamlessly with adambalm server

### Limitations
⚠️ **No Dedicated GPU:** Intel Iris Xe is integrated only  
⚠️ **16GB RAM:** May feel constrained under heavy load  
⚠️ **Single SSD:** No redundancy (rely on git/cloud backups)  
⚠️ **Battery Life:** Moderate (typical ultrabook battery)

### Recommended Workflow
**Use suphouse for:**
- Writing code locally
- Running lightweight tests
- Git operations
- Document creation
- Claude Code interactive sessions
- Remote access to adambalm

**Use adambalm for:**
- GPU-intensive tasks (RTX 5060 Ti 16GB)
- Heavy Docker workloads
- Large database operations
- AI/ML training and inference
- Long-running builds/tests
- Multi-container deployments

**Connection:** `ssh adambalm` (instant, key-based auth)

---

## 🔗 Network Connectivity

### Tailscale Mesh Network
**Tailnet Name:** tail069d40.ts.net  
**This Machine:** suphouse (100.126.163.59)

**Connected Peers:**
- **adambalm** (100.111.114.84) - Ubuntu server, SSH configured ✅
- iphone173 (100.93.129.49) - iOS device
- tattoonows-mac-pro (100.91.110.24) - macOS

**Offline Peers:**
- alexispc (40 days)
- daniel-macbook-pro (105 days)
- eds-imac (12 minutes)
- iphone-13 (21 days)

### SSH Configuration
**Config File:** `~/.ssh/config`

```
Host adambalm
    HostName 100.111.114.84
    User ed
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
```

**Keys:**
- Private: `~/.ssh/id_ed25519` (ED25519, 256-bit)
- Public: `~/.ssh/id_ed25519.pub`
- Fingerprint: SHA256:kPEFiPQ3TBLyeFXUy6wSwpd7pn7KJxfuGeiPvjh0vPk

**Known Hosts:** 2 servers
- 100.111.114.84 (adambalm)
- 100.126.163.59 (self, if needed)

---

## 📝 Comparison with Adambalm

| Feature | Suphouse (Laptop) | Adambalm (Server) |
|---------|-------------------|-------------------|
| **CPU** | i7-1255U (10C/12T, 1.7-4.7GHz) | i5-11400 (6C/12T, 2.6-4.4GHz) |
| **RAM** | 16 GB DDR4-3200 | 64 GB DDR4 |
| **GPU** | Intel Iris Xe (1GB) | RTX 5060 Ti (16GB) |
| **Storage** | 512GB NVMe | 1.8TB LVM (2x 1TB NVMe) |
| **OS** | Windows 11 Home | Ubuntu 24.04 LTS |
| **Form** | Laptop (portable) | Desktop (stationary) |
| **Purpose** | Local development | Heavy workloads, Docker, AI |
| **Uptime** | 9 days | 7 days |
| **GPU Compute** | No CUDA | CUDA 13.0 ✅ |
| **Docker** | Not primary | 14 containers running |

**Strategy:** Use suphouse for coding, adambalm for compute-intensive tasks

---

## 💡 Key Insights

### What Makes This Machine Effective

1. **Modern Architecture:** 12th Gen Intel with hybrid P+E cores optimizes performance vs battery life
2. **Well-Configured:** All development tools pre-installed and configured
3. **Network Integration:** Seamless connection to adambalm via Tailscale + SSH
4. **Adequate Resources:** 16GB RAM and 512GB SSD handle typical dev workloads
5. **Portability:** Laptop form factor enables work anywhere
6. **Security:** VBS, SSH keys, VPN provide multiple security layers

### Development Workflow Optimization

**Local Tasks (Suphouse):**
- Code editing (VS Code, Cursor)
- Git commits and pushes
- Document generation
- Playwright browser tests
- Claude Code sessions
- Light Node.js/Python execution

**Remote Tasks (Adambalm via SSH):**
- Heavy Docker builds
- Database operations
- GPU-accelerated tasks
- Long-running tests
- Multi-container deployments
- AI model inference

**Benefit:** Combines laptop mobility with server power

---

## 🔄 Maintenance Notes

### Regular Tasks
- ✅ Windows Updates applied (4 hotfixes installed)
- ✅ Development tools updated (Claude Code 2.0.47)
- ✅ SSH keys configured and tested
- ✅ Tailscale connection stable

### Recommended Actions
1. **Memory Management:** Monitor RAM usage (currently 83%)
2. **Disk Space:** Keep C: drive below 70% (currently 31% ✅)
3. **Battery Health:** Monitor charge cycles
4. **Backups:** Rely on git + cloud storage (no local redundancy)
5. **Updates:** Keep Windows, drivers, and dev tools current

### Known Issues
- None currently reported

---

## 📚 Documentation References

**Related Notes in Basic Memory:**
- Adambalm Server Specifications (comparison)
- SSH Key Setup Guide (authentication)
- SCA Projects Workspace Documentation
- TennisFlyer Project (Playwright workflow)
- ResumeFactory Project (document generation)

**External Resources:**
- Claude Code Docs: https://docs.claude.com/claude-code
- Playwright Docs: https://playwright.dev
- Tailscale Docs: https://tailscale.com/kb
- Windows 11 Docs: https://docs.microsoft.com/windows

---

**System Specifications Captured:** November 20, 2025 03:00 AM EST  
**Captured By:** Claude Code (Sonnet 4.5) running locally  
**Method:** systeminfo, wmic, network tools, development environment checks  
**Next Review:** As needed for troubleshooting or capacity planning

---

**This is a well-configured laptop for development work with:**
- Modern CPU and adequate RAM for typical tasks
- All development tools installed and configured
- Secure remote access to more powerful server
- Integrated into Tailscale mesh network
- Optimized for local coding + remote execution hybrid workflow
