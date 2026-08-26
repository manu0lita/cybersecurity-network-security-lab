# Networking Basics Notes
**Apex Planet Cybersecurity Internship**

## OSI Model (7 Layers)

| Layer | Name | Function | Example protocols |
|---|---|---|---|
| 7 | Application | Interface for user-facing apps | HTTP, FTP, DNS |
| 6 | Presentation | Data translation, encryption, compression | TLS, JPEG |
| 5 | Session | Establishes/manages sessions between hosts | NetBIOS, RPC |
| 4 | Transport | End-to-end delivery, reliability | TCP, UDP |
| 3 | Network | Logical addressing, routing | IP, ICMP |
| 2 | Data Link | Physical addressing, frames | Ethernet, ARP |
| 1 | Physical | Raw bit transmission over media | Cables, radio, NICs |

## TCP/IP Model

Condenses OSI into 4 layers: Application, Transport, Internet, Network Access.

- **TCP** — connection-oriented, reliable, ordered delivery. Uses a 3-way handshake: `SYN → SYN-ACK → ACK`.
- **UDP** — connectionless, faster, no delivery guarantee. Used for streaming, DNS queries, gaming.

## DNS

- Translates domain names into IP addresses.
- Common record types: `A` (IPv4), `AAAA` (IPv6), `MX` (mail server), `CNAME` (alias), `NS` (nameserver).
- Runs on port 53 (UDP for standard queries, TCP for zone transfers/larger responses).

## HTTP vs HTTPS

- **HTTP** — plaintext, port 80. Anyone on the network path can read it (this is exactly what Burp Suite intercepts).
- **HTTPS** — HTTP wrapped in TLS encryption, port 443. Protects confidentiality and integrity in transit.

## IP Addressing, Subnetting, NAT

- IPv4 address: 32-bit, written as 4 octets (e.g. `192.168.56.101`).
- Private address ranges: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16` (this lab uses `192.168.56.0/24`).
- Subnet mask defines the network vs. host portion of an address — `255.255.255.0` = `/24` = 254 usable host addresses.
- **NAT** (Network Address Translation) lets multiple private IPs share one public IP. This is exactly what Kali's "Adapter 1 (NAT)" does — it gives Kali internet access through the host machine's connection, while staying on a private address internally.

## Applied to This Lab

- Kali (`192.168.56.102`) and Metasploitable (`192.168.56.101`) communicate over the `192.168.56.0/24` Host-Only segment — Layer 3 (IP).
- `ping` uses ICMP, a Layer 3 protocol — this is what the `icmp` Wireshark filter captures.
- `nmap` TCP scans rely on the Layer 4 TCP 3-way handshake — visible under the `tcp` filter as `SYN → SYN-ACK → ACK`.
- Kali's NAT adapter provides internet access; the Host-Only adapter keeps the attack traffic isolated from the internet and the host's real network.
- HTTP traffic to Metasploitable's web apps (port 80) is unencrypted — visible in cleartext in Wireshark and interceptable in Burp Suite.

---
*Documented as part of the Apex Planet Cybersecurity Internship lab.*
