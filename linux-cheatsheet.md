# Linux Command Cheat Sheet
**Kali Linux — Cybersecurity Lab (Apex Planet Internship)**

Quick reference for commands practiced in the isolated Host-Only lab (Kali `192.168.56.102` ↔ Metasploitable2 `192.168.56.101`).

## Navigation & File Management

| Command | Description | Example |
|---|---|---|
| `pwd` | Print current working directory | `pwd` |
| `ls` / `ls -la` | List directory contents (`-la` = all files, long format) | `ls -la` |
| `cd` | Change directory | `cd ~/apex-planet-lab` |
| `mkdir` | Create a new directory | `mkdir linux-practice` |
| `touch` | Create an empty file | `touch test.txt` |
| `cat` | Print file contents to terminal | `cat test.txt` |
| `cp` | Copy a file | `cp test.txt copy.txt` |
| `mv` | Move or rename a file | `mv copy.txt renamed.txt` |
| `rm` | Delete a file | `rm renamed.txt` |

## Permissions & Ownership

| Command | Description | Example |
|---|---|---|
| `ls -l` | Show permissions, owner, group, size | `ls -l test.txt` |
| `chmod` | Change file permissions | `chmod 600 test.txt` |
| `chown` | Change file owner/group | `sudo chown user:group test.txt` |

Numeric permission bits: `r=4, w=2, x=1`, summed per role (owner / group / other).
- `600` → owner: read+write, everyone else: nothing
- `644` → owner: read+write, group/other: read only
- `700` → owner: read+write+execute, everyone else: nothing
- `755` → owner: full access, group/other: read+execute

## System Information

| Command | Description |
|---|---|
| `whoami` | Show the current user |
| `hostname` | Show the machine's hostname |
| `uname -a` | Show kernel and system info |
| `lsb_release -a` | Show OS/distro version |
| `uptime` | Show how long the system has been running |
| `df -h` | Show disk usage, human-readable |
| `free -h` | Show memory usage, human-readable |

## Process Management

| Command | Description |
|---|---|
| `ps` | List current user's processes |
| `ps aux` | List all running processes, all users |
| `top` | Live process monitor (`q` to quit) |

## Networking

| Command | Description | Example |
|---|---|---|
| `ip a` (or `ifconfig`) | Show network interfaces and IPs | `ip a` |
| `ip route` | Show the routing table | `ip route` |
| `ping` | Test connectivity to a host | `ping -c 4 192.168.56.101` |
| `ss -tuln` | Show listening TCP/UDP ports | `ss -tuln` |
| `netstat -tuln` | Legacy equivalent of `ss` | `netstat -tuln` |
| `traceroute` | Show the network path/hops to a host | `traceroute 192.168.56.101` |

## Package Management

| Command | Description | Example |
|---|---|---|
| `sudo apt update` | Refresh the package index | `sudo apt update` |
| `sudo apt install <pkg>` | Install a package | `sudo apt install nmap` |
| `sudo apt remove <pkg>` | Remove a package | `sudo apt remove nmap` |
| `dpkg -l` | List installed packages | `dpkg -l \| grep nmap` |
| `sudo dpkg -i <file.deb>` | Install a local `.deb` package | `sudo dpkg -i package.deb` |

---
*Practiced and documented as part of the Apex Planet Cybersecurity Internship lab.*
