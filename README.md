# Apex Planet Internship – Task 2: Network Security & Scanning

**Repository:** [manu0lita/apex-planet-task-2-network-security](https://github.com/manu0lita/apex-planet-task-2-network-security)  
**Project type:** Practical network-security lab documentation and evidence  
**Lab environment:** Kali Linux and Metasploitable2 on a VirtualBox Host-Only network

## 1. Project overview

This repository documents practical network-security activities completed as part of Apex Planet Internship – Task 2. The work covers network reconnaissance, Nmap scanning and service enumeration, vulnerability assessment with Nessus Essentials, packet inspection with Wireshark, bounded TCP SYN analysis, and host-firewall rule testing with `iptables`.

The project was conducted using a controlled local lab for the hands-on assessment activities. The repository also documents reconnaissance observations associated with a public vulnerability-training host. The public host is included as historical project evidence; this README does not grant permission to scan or test it again.

## 2. Security problem and learning objectives

The project explores how a network administrator or security analyst can:

- Discover reachable hosts and identify exposed TCP/UDP ports.
- Identify services and versions that may require further security review.
- Use vulnerability-scanner results as leads for validation and remediation.
- Inspect HTTP, FTP and DNS traffic to understand what is transmitted over a network.
- Observe TCP SYN/SYN-ACK behaviour using a small, bounded test.
- Apply host-firewall rules and verify their effect from a separate lab host.
- Record evidence and explain the limitations of scanning results.

## 3. Intended users

This is an educational project for cybersecurity and networking students, entry-level network/security analysts, and instructors reviewing introductory network-reconnaissance and defensive-testing exercises. It is not an automated production vulnerability scanner.

## 4. Lab environment and scope

### Controlled local lab

| Component | Details |
|---|---|
| Attacker/analysis VM | Kali Linux |
| Target VM | Metasploitable2 |
| Kali lab address | `192.168.56.102/24` |
| Metasploitable2 lab address | `192.168.56.101/24` |
| Virtual network | VirtualBox Host-Only |
| Main tools | Nmap, Nessus Essentials, Wireshark, hping3, iptables, WHOIS, Nslookup, Shodan and common Linux networking utilities |

### Public training target documented in the report

The original report also records passive and limited reconnaissance observations for `testaspnet.vulnweb.com` (observed IP `44.238.29.244`). These are historical observations from the internship exercise. Do not repeat active testing against any public host unless you have current, explicit authorization and comply with the host owner's rules.

## 5. Work completed and key observations

### Reconnaissance and Nmap

The report documents host discovery, TCP and UDP scanning, service/version detection and OS fingerprinting. For Metasploitable2, 23 open TCP services were observed in the default 1,000-port scan. Service detection included examples such as vsftpd 2.3.4, OpenSSH 4.7p1, Apache 2.2.8, BIND 9.4.2, Samba, MySQL, PostgreSQL, VNC, UnrealIRCd, AJP and Tomcat.

The report records UDP results as `open|filtered` where no response was received. This state is **not proof that a UDP port is open**. OS fingerprinting for the public training target was inconclusive and was not presented as a confirmed operating-system identification.

### Vulnerability assessment

Nessus Essentials was used to assess the Metasploitable2 lab target. The retained report records 59 vulnerabilities on the completed scan dashboard and lists representative findings with their displayed severity/CVSS values. The Nessus export workflow displayed an upgrade requirement, so the retained screenshots are the primary evidence for the results. Scanner findings should be independently checked; a scanner result is not, by itself, proof that an issue is exploitable in every environment.

### Wireshark traffic analysis

The report documents HTTP, FTP and DNS traffic capture and inspection. In the FTP lab exercise, the supplied `msfadmin` account authenticated successfully and the FTP `USER` and `PASS` commands were inspected. This demonstrates why traditional FTP can expose credentials in transit and why encrypted alternatives should be used.

Useful display filters recorded in the report:

```text
ftp.request.command == "USER" || ftp.request.command == "PASS"
```

DNS observations included a `SERVFAIL` response for one query and a successful `NOERROR` response for a localhost A-record query. A failed DNS lookup can still demonstrate DNS request/response traffic; it should not be described as a successful name resolution.

### Bounded TCP SYN analysis

The report records this bounded command against the isolated Metasploitable2 VM:

```bash
sudo hping3 -S -p 80 -c 20 -i u100000 192.168.56.101
```

The documented result was 20 SYN probes sent and 20 SYN-ACK responses received. This demonstrates TCP handshake behaviour for that test; it is **not** evidence of a successful denial-of-service attack.

### Firewall rule validation

The report records a baseline check, a firewall drop rule for TCP/80, and a subsequent Nmap check. The observed change was from `80/tcp open http` to `80/tcp filtered http`.

Example commands from the documented lab test:

```bash
sudo nmap -p 80 192.168.56.101
iptables -I INPUT -p tcp --dport 80 -j DROP
sudo nmap -p 80 192.168.56.101
```

The report also records allowing SSH on TCP/22 and checking ports 22 and 80. Firewall rules can affect connectivity to the target VM; use them only in the isolated lab and ensure you understand how to restore the original rules.

## 6. Repository contents

The public repository currently includes:

- `nmap/` – retained Nmap text-output files.
- `screenshot/` – screenshots supporting the practical work.
- `Apex_Task2_Network_Security_Detailed_Report.md` – detailed report in Markdown.
- `Apex_Task2_Network_Security_Detailed_Report.docx` – editable report.
- `Apex_Task2_Network_Security_Detailed_Report.pdf` – report in PDF format.
- `Task-2-Network-Security-README.md` – earlier task-level notes and workflow.
- `sharkbro.pcapng` – packet capture; inspect for credentials and sensitive data before sharing or retaining it publicly.

The file listing above reflects the repository's visible top-level contents. Refer to the repository itself for the current contents of each folder.

## 7. Sample commands and recorded output

These commands are examples from the existing report and are intended for the isolated Metasploitable2 lab only.

**Baseline check:**

```bash
sudo nmap -p 80 192.168.56.101
```

Recorded output:

```text
80/tcp open http
```

**After applying the documented drop rule:**

```bash
iptables -I INPUT -p tcp --dport 80 -j DROP
sudo nmap -p 80 192.168.56.101
```

Recorded output:

```text
80/tcp filtered http
```

These are transcribed observations from the project report, not a claim that the commands have been rerun as part of this README update.

## 8. Installation and usage

This repository is primarily a collection of lab documentation and evidence. It is not currently packaged as an installable Python application and does not provide a single command that reproduces the entire assessment.

To review the work, clone the repository and open the detailed report and evidence folders:

```bash
git clone https://github.com/manu0lita/apex-planet-task-2-network-security.git
cd apex-planet-task-2-network-security
```

The practical tools listed in this report (such as Nmap, Wireshark, Nessus Essentials, hping3 and iptables) are separate system applications. Their installation and use depend on the operating system and lab setup. Do not run the lab commands against systems you do not own or have permission to assess.

### Planned Round 1 automation extension – not included yet

A possible extension for the Detox Technologies assessment is a local Python utility that parses Nmap XML and creates a structured report. **That utility is not part of the current repository contents described above.** Do not claim that it is implemented, tested or runnable until its source code, sample XML, expected output and tests have actually been added and verified. If it is added, document its exact command and test results here.

## 9. Security considerations

- Perform active scanning and firewall experiments only on systems you own or are explicitly authorized to test.
- Keep the Metasploitable2 exercises isolated on the Host-Only network.
- Do not publish passwords, tokens, private data or unredacted credential-bearing packet captures.
- The repository currently lists `sharkbro.pcapng` at its root. Inspect the capture before public submission. If it contains FTP usernames/passwords or other sensitive information, remove it from the public repository and ensure the sensitive data is not still exposed in Git history; replace it only with a sanitized capture if appropriate.
- Treat Nmap and Nessus observations as leads for investigation, not automatic proof of exploitability.
- Do not classify `open|filtered` UDP results as confirmed open ports.
- Do not describe the bounded 20-packet SYN test as a denial-of-service demonstration.
- Avoid publishing real credentials even when they were used only in a deliberately vulnerable lab.

## 10. Known limitations

- Results describe the lab and scan conditions at the time the exercises were performed; they are not a current assessment of any host.
- Service banners and version strings can be incomplete, inaccurate or insufficient to establish vulnerability.
- UDP `open|filtered` states are ambiguous.
- The retained Nessus export was not available in the documented session; screenshots are the primary evidence for its dashboard findings.
- The repository is documentation/evidence rather than a unified automated scanner or reporting application.
- A public packet capture may contain sensitive authentication data and must be reviewed before distribution.

## 11. Future improvements

- Add a locally runnable Nmap XML parser that produces a Markdown report.
- Add sample XML input, expected output and automated tests, including ambiguous and malformed-input cases.
- Add a test showing that an open service is not automatically labelled vulnerable without supporting evidence.
- Add a sanitized packet capture or a written note if the existing capture cannot safely be shared.
- Add a short demonstration video showing the lab evidence and, if implemented, the new utility.

## 12. References

- [Nmap Reference Guide](https://nmap.org/book/)
- [Nmap Port Scanning Basics](https://nmap.org/book/man-port-scanning-basics.html)
- [Tenable Nessus Documentation](https://docs.tenable.com/nessus/Content/GettingStarted.htm)

---

**Accuracy note:** This README summarizes the existing repository and its detailed project report. It intentionally distinguishes completed internship activities from any future automation added for the Detox Technologies assessment.
