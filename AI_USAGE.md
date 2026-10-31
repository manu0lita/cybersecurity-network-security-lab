# AI Usage Disclosure

**Project:** Apex Planet Internship – Task 2: Network Security & Scanning  
**Disclosure scope:** Preparation of the project documentation for the Detox Technologies Round 1 assessment, dated 31 October 2026.

This disclosure covers the AI assistance I used while learning, troubleshooting and documenting the Apex Planet network-security exercises, as well as preparing the current Detox Technologies assessment documents. Before submitting, I will add any further AI tools or code-generation/debugging assistance used during the assessment.

## 1. Which AI tools did I use?

- **ChatGPT (OpenAI):** Used during preparation of the Detox Technologies assessment materials.

If I use any other AI tool while completing the assessment, I will add its name and describe how it was used here.

## 2. How did AI assist me?

ChatGPT assisted with:

- Explaining networking and security concepts relevant to the practical exercises.
- Helping me understand and troubleshoot parts of the lab setup and command-line workflow.
- Explaining Nmap, Nessus, Wireshark, hping3 and `iptables` commands and helping interpret outputs that I shared for review.
- Reviewing the publicly visible structure and existing Markdown report of my Apex Planet Task 2 repository.
- Organising the existing lab activities into a clearer project README.
- Identifying documentation and submission gaps against the Detox Technologies task instructions.
- Suggesting a possible future Nmap XML-to-Markdown reporting utility as a small automation extension.

AI assistance was used for learning, troubleshooting, interpretation and documentation. The existing scan observations and lab evidence are described from my internship report and repository. ChatGPT did not independently access my lab, execute the historical scans or generate the original packet capture; I ran the lab commands and collected the evidence in my environment.

## 3. Which parts were generated or substantially suggested by AI?

- Explanations, troubleshooting suggestions and interpretation guidance for some networking/security commands and outputs were provided by ChatGPT during my learning process.
- The current `README.md` wording and organisation were substantially drafted with ChatGPT assistance.
- This `AI_USAGE.md` disclosure was drafted with ChatGPT assistance.
- The idea of adding a local Nmap XML report generator was suggested during the assessment-planning discussion. **That suggestion is not evidence that the utility has been implemented.**

The historical Nmap, Nessus, Wireshark, hping3 and firewall observations are summarized from the project's existing report. They must not be represented as AI-generated test results.

## 4. What mistakes, insecure suggestions or incorrect assumptions did AI make?

During planning, an Nmap XML report generator was discussed as the recommended extension. It was necessary to distinguish a proposed feature from an existing, working program. The current repository should not claim that this utility exists until its source code and tests are added and executed.

I also need to avoid these common interpretation errors when reviewing AI suggestions or scan output:

- An open port or service banner alone does not prove that the service is vulnerable.
- Nmap's UDP state `open|filtered` is ambiguous and must not be reported as confirmed open.
- A bounded SYN/SYN-ACK test is not proof of a denial-of-service condition.
- A Nessus finding requires review and, where possible, independent validation; a scanner result is not automatically proof of exploitability.

If further AI-generated code or analysis introduces an error, I will record the specific error and correction here rather than leaving this section generic.

## 5. How did I manually validate AI-generated content or output?

For the documentation update, I compared the project descriptions and reported observations against the existing `Apex_Task2_Network_Security_Detailed_Report.md` and the files visible in my public GitHub repository. During the practical work, I ran commands in my own lab and used the resulting terminal output, scan files and screenshots as the evidence recorded in the repository; AI explanations were used as guidance, not as a substitute for running the tests.

The existing report records, among other details:

- The VirtualBox Host-Only lab addresses used for Kali and Metasploitable2.
- The 23 open TCP services observed on Metasploitable2 in the documented default 1,000-port scan.
- The 59-vulnerability count shown on the completed Nessus Essentials dashboard.
- Wireshark inspection of HTTP, FTP and DNS traffic.
- The bounded test of 20 SYN probes and 20 SYN-ACK responses.
- The change in the observed TCP/80 state after applying the documented `iptables` drop rule.

The documentation was written to preserve the report's stated limitations. I have not treated this documentation review as a fresh execution or independent reproduction of those historical results.

**Validation still required before final submission:** I must inspect the public PCAP for credentials or sensitive data, verify the repository's original commit dates, and run any new utility and its tests myself before claiming that it works.

## 6. What did I change after reviewing AI-assisted work?

- Kept the existing Apex Planet internship work separate from the proposed Detox assessment extension.
- Did not claim that an Nmap XML parser, automated report generator or its tests are already present.
- Preserved the distinction between an ambiguous UDP `open|filtered` result and a confirmed open port.
- Preserved the report's qualification that the 20-packet SYN test is not a denial-of-service demonstration.
- Added a warning that the repository's `sharkbro.pcapng` file must be checked for FTP credentials and other sensitive information before public distribution.
- Clarified that the observations are historical lab results and are not a current scan of any target.

## 7. Which parts of the final project can I explain without AI assistance?

I should be able to explain the practical lab work documented in my report, including:

- The purpose of the VirtualBox Host-Only network and the roles of the Kali and Metasploitable2 VMs.
- The difference between Nmap TCP SYN scanning, UDP scanning, service/version detection and OS fingerprinting.
- Why `open|filtered` is not the same as confirmed `open` for UDP scanning.
- How Nessus findings are used as leads for vulnerability investigation and why they require validation.
- How Wireshark display filters were used to inspect FTP authentication traffic and why plaintext FTP is risky.
- What the bounded hping3 SYN test demonstrated and what it did not demonstrate.
- How the documented `iptables` rule changed the observed accessibility of TCP/80.

I will only retain claims in this section that I can personally explain during a live technical verification. If an Nmap XML utility is added, I will also update this disclosure to identify any AI-assisted code, explain its parsing logic, and document the tests I personally ran.

---

**Candidate review before submission:** This file is a disclosure draft. Before sending it, I must check that it accurately covers every AI tool and every form of assistance used throughout the internship project (including any code-generation or debugging help), and correct any wording that does not match what I actually did.
