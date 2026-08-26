# Cybersecurity Basics Notes
**Apex Planet Cybersecurity Internship**

## The CIA Triad

- **Confidentiality** — ensuring only authorized parties can access data. Enforced via encryption, access controls, authentication.
- **Integrity** — ensuring data isn't altered or tampered with, whether in transit or at rest. Enforced via hashing, digital signatures, checksums.
- **Availability** — ensuring systems and data are accessible when needed. Enforced via redundancy, backups, DDoS protection.

## Threat Types

- **Phishing** — social engineering via fraudulent emails/messages to steal credentials or deliver malware.
- **Malware** — malicious software (viruses, worms, trojans, spyware) designed to damage or exploit systems.
- **DDoS (Distributed Denial of Service)** — overwhelming a system with traffic from many sources to make it unavailable.
- **SQL Injection** — injecting malicious SQL through input fields to manipulate or extract database contents.
- **Brute Force** — systematically trying credential combinations until one succeeds.
- **Ransomware** — malware that encrypts a victim's data and demands payment for the decryption key.

## Attack Vectors

- **Social Engineering** — manipulating people rather than systems into revealing information or granting access (phishing, pretexting, baiting).
- **Wireless Attacks** — exploiting weak Wi-Fi security, rogue access points, or packet sniffing over wireless networks.
- **Insider Threats** — malicious or negligent actions by someone with legitimate access, such as an employee or contractor.

## Applied to This Lab

- Metasploitable2 is intentionally loaded with outdated, vulnerable services (e.g. the vsftpd 2.3.4 backdoor, weak Samba configuration) — a hands-on demonstration of how unpatched software directly threatens Confidentiality and Integrity.
- Nmap scanning mirrors the reconnaissance phase an attacker performs before selecting an attack vector.
- The isolated Host-Only network models a safe environment to study these threats without risking the Availability or Confidentiality of any real system.

---
*Documented as part of the Apex Planet Cybersecurity Internship lab.*
