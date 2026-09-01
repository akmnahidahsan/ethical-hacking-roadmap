# 🐧 Linux Fundamentals Cheatsheet

> Reference for navigation, permissions, and system basics. Practice in your own lab or authorized environment.

---

## Navigation & Files

| Command | Purpose |
|---|---|
| `pwd` | Show current directory |
| `ls -la` | List all files, including hidden, with details |
| `cd /path` | Change directory |
| `find / -name "filename"` | Search for a file by name |
| `find / -perm -4000 2>/dev/null` | Find SUID binaries |
| `locate filename` | Fast file search (needs `updatedb`) |
| `file filename` | Identify file type |
| `tree` | Visual directory structure |

## Permissions

```
rwxr-xr-x
│││ │  └── others: r-x
│││ └───── group:  r-x
└────────── owner:  rwx
```

| Command | Purpose |
|---|---|
| `chmod 755 file` | Set permissions numerically |
| `chmod u+x file` | Add execute for owner |
| `chown user:group file` | Change ownership |
| `umask` | Show default permission mask |
| `stat file` | Detailed file metadata |

**Special bits:** SUID (`4000`), SGID (`2000`), Sticky bit (`1000`) — understand these before touching `13-linux-security.md`.

## Users & Groups

| Command | Purpose |
|---|---|
| `whoami` / `id` | Current user and group memberships |
| `cat /etc/passwd` | List system users |
| `cat /etc/group` | List groups |
| `sudo -l` | Show sudo privileges for current user |
| `su - username` | Switch user |
| `useradd` / `usermod` / `userdel` | Manage users (root) |

## Processes & Services

| Command | Purpose |
|---|---|
| `ps aux` | List running processes |
| `top` / `htop` | Live process monitor |
| `kill -9 PID` | Force kill a process |
| `systemctl status service` | Check service status |
| `systemctl list-units --type=service` | List all services |
| `journalctl -xe` | Recent system logs |

## Networking Basics

| Command | Purpose |
|---|---|
| `ip a` | Show interfaces and IPs |
| `ss -tulnp` | Show listening ports and owning process |
| `netstat -antp` | Legacy equivalent of `ss` |
| `curl -I URL` | Fetch response headers |
| `dig domain` | DNS lookup |

## Package Management

| Distro | Install | Update | Search |
|---|---|---|---|
| Debian/Ubuntu | `apt install pkg` | `apt update && apt upgrade` | `apt search pkg` |
| RHEL/Fedora | `dnf install pkg` | `dnf update` | `dnf search pkg` |
| Arch | `pacman -S pkg` | `pacman -Syu` | `pacman -Ss pkg` |

## Logs Worth Knowing

| Path | Contents |
|---|---|
| `/var/log/auth.log` (Debian) / `/var/log/secure` (RHEL) | Authentication attempts |
| `/var/log/syslog` | General system log |
| `/var/log/apache2/` or `/var/log/nginx/` | Web server logs |
| `~/.bash_history` | Shell command history |

## Bash Quick Reference

```bash
# Redirect output
cmd > file.txt      # overwrite
cmd >> file.txt     # append
cmd 2>&1             # merge stderr into stdout

# Loops
for i in $(seq 1 5); do echo $i; done

# Piping
ps aux | grep nginx

# Background job
long_task &
jobs
fg %1
```

---

**Related:** [Linux roadmap phase](../roadmap/02-linux.md) · [Linux Security phase](../roadmap/13-linux-security.md)
