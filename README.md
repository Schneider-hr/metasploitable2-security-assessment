# Security Assessment of a Deliberately Vulnerable Lab System (Metasploitable 2)

A team security assessment completed as part of the **Thrive Africa Cybersecurity Internship 2026 (Group 8)**, an eight-week, structured training program using simulated and lab targets — not a real client engagement. The target was **Metasploitable 2**, a Linux virtual machine that is intentionally built to be vulnerable and distributed specifically for security training, run in an isolated VirtualBox lab against a Kali Linux attacking machine. No real systems, clients, or production infrastructure were involved.

This page covers **my individual contribution** to the assessment. The full engagement was a group deliverable; the vulnerability assessment and risk analysis stages were completed by my teammates and aren't reproduced here — see the summary below for how the pieces fit together.

## My contribution

**Reconnaissance and network enumeration (Week 2).** Using Kali Linux and Nmap against the Metasploitable 2 target, I ran host discovery, port scanning, service/version enumeration, and OS fingerprinting to build a full picture of the target's exposed attack surface before any exploitation was attempted — the standard "know what's actually running before you touch it" discipline. The scan identified a broad set of open ports and running services (including web, database, file-sharing, and remote-access services), consistent with Metasploitable 2's known design as an intentionally exposed training target.

**Security governance (Week 5).** Wrote five security policies for a simulated organization — covering information security, access control, password management, incident reporting, and acceptable use — along with defined security roles and responsibilities. This is the governance layer that sits above the technical findings: policy that gives the technical controls somewhere to plug into.

**Incident response playbook (Week 6).** Wrote an incident response playbook following the **NIST SP 800-61 Rev. 2** framework, including three specific scenario playbooks mapped to realistic incident types an organization running a system like this could face.

## Done by my teammates as part of the group

**Vulnerability assessment (Week 3).** Identified known CVEs affecting the target's exposed services, cross-referenced against the NIST National Vulnerability Database, plus a set of web-application findings from Nikto against the target's web service.

**Risk analysis (Week 4).** Built a risk register from the vulnerability assessment findings, prioritized by severity, with a remediation roadmap.

## Tools

Kali Linux, Nmap, Nikto, NIST National Vulnerability Database.

## A note on scope

In line with the training program's own confidentiality terms, this page stays at the level of method and outcome rather than reproducing raw scan output, lab IP addresses, or the full original report — the goal is to document the real work and real skills exercised without publishing internal lab data that doesn't add anything for a reader anyway. The Metasploitable 2 target itself is a widely used, publicly documented training VM, freely available for anyone to practice against.
