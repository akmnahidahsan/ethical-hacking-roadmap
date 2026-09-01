# 🌐 Networking Fundamentals Cheatsheet

> Core concepts to understand before scanning, enumeration, or traffic analysis.

---

## OSI Model (top to bottom)

| Layer | Name | Examples |
|---|---|---|
| 7 | Application | HTTP, DNS, FTP, SSH |
| 6 | Presentation | TLS/SSL, encoding |
| 5 | Session | Sessions, sockets |
| 4 | Transport | TCP, UDP |
| 3 | Network | IP, ICMP, routing |
| 2 | Data Link | MAC addresses, switches |
| 1 | Physical | Cables, radio, NICs |

## TCP vs UDP

| | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented (handshake) | Connectionless |
| Reliability | Guaranteed delivery, ordered | Best-effort, no order guarantee |
| Speed | Slower (overhead) | Faster |
| Use cases | HTTP, SSH, FTP | DNS, DHCP, streaming, VoIP |

## TCP 3-Way Handshake

```
Client → SYN     → Server
Client ← SYN-ACK ← Server
Client → ACK     → Server
```
Understanding this explains why Nmap's SYN scan (`-sS`) is called a "half-open" scan.

## Common Ports

| Port | Service |
|---|---|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |
| 5432 | PostgreSQL |
| 8080 | HTTP (alt) |

## IP Addressing & Subnetting

```
CIDR   Subnet Mask       Hosts
/24    255.255.255.0     254
/25    255.255.255.128   126
/26    255.255.255.192   62
/27    255.255.255.224   30
/28    255.255.255.240   14
/30    255.255.255.252   2
```

Private ranges (RFC 1918):
```
10.0.0.0    – 10.255.255.255   (10/8)
172.16.0.0  – 172.31.255.255   (172.16/12)
192.168.0.0 – 192.168.255.255  (192.168/16)
```

## DNS Record Types

| Record | Purpose |
|---|---|
| A | Domain → IPv4 |
| AAAA | Domain → IPv6 |
| CNAME | Alias to another domain |
| MX | Mail server |
| TXT | Arbitrary text (SPF, verification, etc.) |
| NS | Authoritative name servers |
| PTR | Reverse lookup (IP → domain) |

## Useful Commands

| Command | Purpose |
|---|---|
| `ip a` / `ifconfig` | Show interfaces |
| `ip route` | Show routing table |
| `dig domain.com ANY` | Full DNS record dump |
| `dig -x IP` | Reverse DNS lookup |
| `traceroute domain.com` | Path to destination |
| `tcpdump -i eth0 -n` | Live packet capture |
| `whois domain.com` | Domain registration info |

## Packet Capture Basics (Wireshark/tcpdump)

- Filter by host: `host 192.168.1.10`
- Filter by port: `tcp port 443`
- Filter by protocol: `dns` or `http`
- Combine: `tcp and port 80 and host 10.0.0.5`

---

**Related:** [Networking roadmap phase](../roadmap/03-networking.md) · [Scanning & Enumeration phase](../roadmap/07-scanning-enumeration.md)
