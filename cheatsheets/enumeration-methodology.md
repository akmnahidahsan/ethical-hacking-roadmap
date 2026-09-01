# 🔎 Enumeration Methodology Cheatsheet

> Systematic approach to mapping an authorized target's attack surface before assessment.

---

## Why Enumeration Matters

Enumeration is the difference between guessing and testing with evidence. A missed subdomain, an unlisted vhost, or an unenumerated service is a missed finding. Work methodically, not randomly.

## General Order of Operations

```
Passive Recon → Active Recon → Service Enumeration → Deep Enumeration → Validation
```

## 1. Subdomain Enumeration

| Tool | Purpose |
|---|---|
| `amass enum -d target.com` | Passive + active subdomain discovery |
| `subfinder -d target.com` | Fast passive subdomain enumeration |
| `httpx -l subdomains.txt` | Probe which subdomains are alive |
| Certificate transparency (`crt.sh`) | Historical subdomains from SSL certs |

## 2. DNS Enumeration

```bash
dig target.com ANY
dig target.com MX
dig target.com TXT
dig -x IP                    # reverse lookup
nslookup target.com
```

## 3. Port & Service Enumeration

```bash
nmap -p- -sV -oA full_scan target.com
```
See [nmap-concepts.md](nmap-concepts.md) for scan-type details.

## 4. Web Directory & File Enumeration

| Tool | Purpose |
|---|---|
| `ffuf -w wordlist.txt -u https://target.com/FUZZ` | Fast directory/file fuzzing |
| `gobuster dir -u https://target.com -w wordlist.txt` | Directory brute-forcing |
| `feroxbuster -u https://target.com` | Recursive content discovery |

Common wordlists: SecLists' `common.txt`, `raft-medium-directories.txt`.

## 5. Service-Specific Enumeration

| Service | Approach |
|---|---|
| SMB (445) | `smbclient -L //target/`, `enum4linux -a target`, `netexec smb target` |
| SNMP (161) | `snmpwalk -c public -v1 target` |
| SMTP (25) | `VRFY`/`EXPN` username enumeration checks |
| FTP (21) | Check for anonymous login |
| HTTP(S) | Banner grab with `curl -I`, check `robots.txt`, `/.well-known/` |

## 6. User & Credential Enumeration (Active Directory)

| Tool | Purpose |
|---|---|
| `bloodhound-python` | Map AD relationships and attack paths |
| `netexec` (formerly CrackMapExec) | Validate credentials across hosts |
| `kerbrute userenum` | Enumerate valid AD usernames via Kerberos |

See [Active Directory phase](../roadmap/16-active-directory.md) for the full methodology.

## 7. OSINT-Layer Enumeration

- Company structure and naming conventions (for username pattern guessing)
- Public code repositories for leaked config/secrets
- Job postings for tech stack disclosure
- Metadata in public documents (`exiftool`)

## Enumeration Tracking Template

Keep a running note per target:

```
Host: 
IP: 
Open ports: 
Services + versions: 
Discovered subdomains: 
Discovered directories: 
Interesting findings: 
Next steps: 
```

---

**Related:** [Reconnaissance & OSINT phase](../roadmap/06-reconnaissance-osint.md) · [Scanning & Enumeration phase](../roadmap/07-scanning-enumeration.md)
