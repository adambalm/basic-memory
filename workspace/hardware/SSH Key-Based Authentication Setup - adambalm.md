---
title: SSH Key-Based Authentication Setup - adambalm
type: note
permalink: workspace/hardware/ssh-key-based-authentication-setup-adambalm
tags:
- ssh
- authentication
- adambalm
- tailscale
- security
- setup
---

# SSH Key-Based Authentication Setup - adambalm Server

## Configuration Date
November 20, 2025

## Setup Summary
Configured persistent, password-less SSH authentication from suphouse (Windows) to adambalm (Linux) server.

## What Was Done

### 1. Generated SSH Key Pair
```bash
ssh-keygen -t ed25519 -C "guest1@suphouse" -f ~/.ssh/id_ed25519 -N ""
```

**Key Details:**
- Type: ED25519 (modern, secure)
- Location: `~/.ssh/id_ed25519` (private key)
- Public key: `~/.ssh/id_ed25519.pub`
- Fingerprint: `SHA256:kPEFiPQ3TBLyeFXUy6wSwpd7pn7KJxfuGeiPvjh0vPk`
- Comment: `guest1@suphouse`

### 2. Copied Public Key to Remote Server
```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub ed@100.111.114.84
```

Public key added to: `/home/ed/.ssh/authorized_keys` on adambalm

### 3. Created SSH Config File
**Location:** `~/.ssh/config`

**Contents:**
```
# SSH Configuration for Guest1@suphouse

# Adambalm server (via Tailscale)
Host adambalm
    HostName 100.111.114.84
    User ed
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes

# Default settings
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

## How to Connect

### Simple Connection
```bash
ssh adambalm
```

No password needed! Just type `ssh adambalm` and you're in.

### Full Connection (if needed)
```bash
ssh ed@100.111.114.84
```

### From Claude Code
I can now run commands on adambalm without any authentication prompts:
```bash
ssh adambalm "cd ~/sca && git status"
ssh adambalm "docker ps"
ssh adambalm "ls -la ~"
```

## Testing Results

### Before Setup
- Authentication method: **password**
- Credentials cached in Windows Credential Manager
- No SSH keys present
- No SSH agent running

### After Setup ✅
- Authentication method: **publickey (ed25519)**
- No password prompts
- Persistent, secure authentication
- Works from Claude Code sessions
- Simplified connection via hostname alias

## SSH Directory Contents

```
~/.ssh/
├── config               # SSH client configuration
├── id_ed25519          # Private key (keep secret!)
├── id_ed25519.pub      # Public key (safe to share)
└── known_hosts         # Known host fingerprints
```

## Security Notes

### Private Key Security
- **Never share** the private key (`id_ed25519`)
- File permissions: Should be readable only by you
- No passphrase set (for automation - acceptable on trusted machine)

### Public Key
- Safe to distribute (`id_ed25519.pub`)
- Currently installed on: adambalm server
- Can be added to additional servers as needed

### Tailscale Integration
- Connection goes over Tailscale VPN (100.x.x.x range)
- Encrypted tunnel between machines
- SSH on top of Tailscale provides defense-in-depth

## Benefits

### For Interactive Use
- Type `ssh adambalm` - instant connection
- No password prompts
- Shorter command

### For Claude Code
- Seamless remote command execution
- No authentication interruptions
- Can run scripts and automation
- Read/analyze remote codebases
- Transfer files easily

### For Automation
- Cron jobs can connect without passwords
- Scripts won't hang on auth prompts
- Reliable CI/CD connections

## Troubleshooting

### If Connection Fails
1. Check Tailscale is running: `tailscale status`
2. Verify server is online: `100.111.114.84`
3. Test explicit key: `ssh -i ~/.ssh/id_ed25519 ed@100.111.114.84`
4. Check permissions: `ls -la ~/.ssh/id_ed25519` (should be 600)

### If Permission Denied
- Verify public key on remote: `ssh adambalm "cat ~/.ssh/authorized_keys"`
- Check remote permissions: `ssh adambalm "ls -la ~/.ssh/"`
- Remote authorized_keys should be 600 or 644

### Re-generate If Needed
```bash
# On local machine
ssh-keygen -t ed25519 -C "guest1@suphouse" -f ~/.ssh/id_ed25519

# Copy to remote
ssh-copy-id -i ~/.ssh/id_ed25519.pub ed@100.111.114.84
```

## Connection Examples

### Simple Commands
```bash
ssh adambalm hostname
ssh adambalm uptime
ssh adambalm "whoami && pwd"
```

### Project Work
```bash
ssh adambalm "cd ~/sca && git status"
ssh adambalm "docker exec springfield_academy_django python manage.py check"
```

### File Transfer
```bash
# Download from remote
scp adambalm:~/sca/file.txt ./

# Upload to remote
scp ./local-file.txt adambalm:~/sca/
```

## Additional Servers

To add this key to other servers:
```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server
```

Then add to `~/.ssh/config`:
```
Host servername
    HostName ip.or.hostname
    User username
    IdentityFile ~/.ssh/id_ed25519
```

## Status
✅ **Working perfectly** - Tested and verified November 20, 2025

---

**Setup completed by:** Claude Code (Sonnet 4.5)  
**Local machine:** suphouse (Guest1@SUPHOUSE)  
**Remote server:** adambalm (ed@100.111.114.84)  
**Connection method:** Tailscale VPN + SSH keys
