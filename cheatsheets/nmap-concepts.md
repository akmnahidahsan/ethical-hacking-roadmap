# 🔍 Nmap Concepts Cheatsheet

> Scanning concepts and syntax for **authorized environments only**. Never scan systems without explicit written permission.

---

## Scan Types

| Flag | Name | Notes |
|---|---|---|
| `-sS` | TCP SYN scan | Default for privileged users, "half-open," fast and stealthier |
| `-sT` | TCP Connect scan | Full handshake, used when SYN isn't available (unprivileged) |
| `-sU` | UDP scan | Slower, often needed for DNS/SNMP/DHCP discovery |
| `-sV` | Version detection | Identifies service/version banners |
| `-sC` | Default script scan | Runs safe NSE scripts |
| `-O` | OS detection | Fingerprints the target OS |
| `-sn` | Ping scan (host discovery only) | No port scan, just checks if hosts are up |
| `-A` | Aggressive | Combines `-O -sV -sC --traceroute` |

## Target Specification

```bash
nmap 192.168.1.1                  # single host
nmap 192.168.1.0/24               # CIDR range
nmap 192.168.1.1-50               # range
nmap -iL targets.txt              # from file
```

## Port Selection

| Flag | Purpose |
|---|---|
| `-p 80,443` | Specific ports |
| `-p 1-1000` | Port range |
| `-p-` | All 65535 ports |
| `-F` | Fast scan (top 100 ports) |
| `--top-ports 20` | Scan N most common ports |

## Timing Templates

| Flag | Speed | Use case |
|---|---|---|
| `-T0` | Paranoid | Max stealth, very slow (IDS evasion labs) |
| `-T2` | Polite | Reduces load on target |
| `-T3` | Normal | Default |
| `-T4` | Aggressive | Common for CTFs/labs with permission |
| `-T5` | Insane | Fastest, easily detected, unreliable results |

## Output Formats

```bash
nmap -oN scan.txt target      # normal
nmap -oX scan.xml target      # XML (parseable)
nmap -oG scan.gnmap target    # grepable
nmap -oA scan_basename target # all formats at once
```

## NSE (Nmap Scripting Engine) Basics

```bash
nmap --script=default target
nmap --script=vuln target              # known vulnerability checks
nmap --script=http-title target
nmap --script-help=http-enum
ls /usr/share/nmap/scripts/ | grep http   # browse available scripts
```

Script categories: `auth`, `default`, `discovery`, `intrusive`, `safe`, `vuln`.

## Example Workflows

```bash
# Host discovery on a subnet
nmap -sn 192.168.1.0/24

# Full TCP port sweep, save all formats
nmap -p- -oA full_scan 192.168.1.10

# Service/version detection on discovered ports
nmap -sV -sC -p 22,80,443 192.168.1.10

# UDP scan of common UDP services
nmap -sU --top-ports 20 192.168.1.10
```

## Firewall/IDS Evasion Flags (know these conceptually — for authorized red-team labs only)

| Flag | Purpose |
|---|---|
| `-f` | Fragment packets |
| `-D RND:10` | Decoy scan with random IPs |
| `--source-port 53` | Spoof source port |
| `--data-length 25` | Pad packets |

> These are documented for understanding detection mechanisms in defensive exercises, not for use outside authorized scope.

---

**Related:** [Scanning & Enumeration phase](../roadmap/07-scanning-enumeration.md)
