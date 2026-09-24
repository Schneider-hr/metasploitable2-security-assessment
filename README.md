# Security Assessment of a Deliberately Vulnerable Lab System (Metasploitable 2)

A team security assessment completed as part of the **Thrive Africa Cybersecurity Internship 2026 (Group 8)**, an eight-week, structured training program using simulated and lab targets — not a real client engagement. The target was **Metasploitable 2**, a Linux virtual machine that is intentionally built to be vulnerable and distributed specifically for security training, run in an isolated VirtualBox lab against a Kali Linux attacking machine. No real systems, clients, or production infrastructure were involved.

This page covers **my individual contribution** to the assessment. The full engagement was a group deliverable; the vulnerability assessment and risk analysis stages were completed by my teammates and aren't reproduced here — see the summary below for how the pieces fit together.

## My contribution

### Week 2 — Reconnaissance and network enumeration

Using Kali Linux and Nmap against the Metasploitable 2 target, I worked through the standard reconnaissance sequence rather than jumping straight to exploitation: connectivity verification, a host-discovery sweep of the lab subnet, a full TCP port scan, service/version enumeration (`nmap -sV`) to identify exactly what software was running behind each open port, an aggressive scan (`-A`) combining OS fingerprinting with default NSE scripts, and a dedicated full 65535-port sweep to rule out anything missed by the default scan range. I closed the exercise with an attack-surface summary — grouping the discovered services by the category of risk they represent (remote administration, file transfer, web, database, file-sharing) rather than just listing them, since that's the framing that actually feeds into a risk assessment. The scan identified 24 open ports in total, consistent with Metasploitable 2's known design as an intentionally exposed training target.

### Week 5 — Security governance and policy development

Working from the vulnerability and risk findings my teammates produced in Weeks 3–4, I built the governance layer that sits above the technical findings — the layer that turns "we found problems" into "here's who's accountable for fixing them and how."

**Roles and governance structure.** I defined five roles aligned to ISO/IEC 27001 principles: an Information Security Officer (policy ownership and risk oversight, reporting to the Board), a System Administrator (implements technical controls, patch SLAs, account management), a Data Custodian (data classification, backup integrity, access auditing), an Information Asset Owner (business-level risk acceptance for their assets), and General Users (compliance, incident reporting, credential hygiene). I mapped these into a governance hierarchy and a decision-rights matrix (who can approve, implement, or must simply be informed for each type of security decision) and defined a five-step escalation path from first detection through to regulatory notification.

**Five policies**, each with a defined owner, scope, and review cycle, and each explicitly linked back to specific findings from the risk register so nothing identified earlier in the engagement was left unaddressed at the governance level:
- **Information Security Policy** — the overarching policy establishing guiding principles (least privilege, defence in depth, need-to-know, accountability, risk-based prioritization, transparent incident reporting) that every other policy sits under.
- **Access Control Policy** — account provisioning rules, authentication requirements (mandatory MFA for privileged/remote access), privileged-access logging, and a per-service table of required network-level controls for the specific services the assessment had flagged as risky.
- **Password Policy** — tiered password requirements by account type (general user, administrative, service account, database, remote-desktop), password protection rules, and mandatory MFA scope.
- **Incident Reporting Policy** — defines what counts as a security incident, a four-level severity scale with response-time targets, a five-step reporting procedure for staff, and a no-blame reporting culture (while still treating failure to report as a disciplinary matter).
- **Acceptable Use Policy** — permitted vs. prohibited use of organizational systems, BYOD minimum security standards, and monitoring/privacy terms.

I finished with a risk-to-policy traceability matrix mapping every item in the Week 4 risk register to the specific policy section that addresses it, plus a glossary and staff acknowledgement record.

### Week 6 — Incident response playbook (NIST SP 800-61 Rev. 2)

Built on top of the governance framework from Week 5, this is the operational document for when something actually goes wrong. I structured it around the four-phase NIST SP 800-61 Rev. 2 lifecycle, expanded into six practical phases: **Preparation** (log management, IDS tuning, backup testing, tabletop exercises), **Detection & Identification** (detection sources, a step-by-step identification procedure, and an indicators-of-compromise reference table for the specific services the assessment had flagged), **Containment** (short-term — network isolation, evidence preservation — vs. long-term — organization-wide firewall rules, heightened monitoring), **Eradication** (removing backdoors and unauthorized software, closing ports at both firewall and OS level, credential rotation, patching in priority order, checking for persistence mechanisms), **Recovery** (independently-verified clean state, backup integrity checks, a mandatory 48-hour monitored reconnection period before declaring an incident closed), and **Post-Incident Review** (a structured lessons-learned process feeding back into the risk register and the policies from Week 5).

I also defined a severity classification system (Critical/High/Medium/Low, each with its own response-time target and notification authority), a communication and escalation plan with a concrete notification timeline, and **three scenario-specific playbooks**, each following the same Detect → Contain → Eradicate → Recover structure: one for backdoor/root-shell-type exploitation, one for credential theft and unauthorized remote access, and one for data exfiltration via an unauthorized file-sharing/database access path. The playbook closes with a printable quick-reference card and a incident-response checklist for critical/high-severity events.

### Week 7 — Passive OSINT exposure assessment

I ran a passive open-source intelligence (OSINT) exercise against a real, public organization — gathering only information that was already publicly available (DNS records, public web presence, standard OSINT reconnaissance techniques), with no systems accessed, no credentials tested, and no active scanning of anything outside the Metasploitable 2 lab.

I'm intentionally not naming the organization or detailing the findings here. This exercise surfaced real, unpatched, security-relevant information about a live third party rather than the lab VM everything else on this page covers, and that isn't mine to publish. The findings were shared only within the internship program itself, and any responsible next step (notifying the organization) would go through a private channel, not a public repo.

### Week 8 — Final report and project showcase

I consolidated the full eight-week engagement — reconnaissance, the vulnerability assessment and risk analysis my teammates led, the governance policies and incident-response playbook above, and the Week 7 OSINT exercise — into a final written report and a presentation deck, and delivered the showcase live to the internship cohort.

## Done by my teammates as part of the group

**Vulnerability assessment (Week 3).** Identified known CVEs affecting the target's exposed services, cross-referenced against the NIST National Vulnerability Database, plus a set of web-application findings from Nikto against the target's web service.

**Risk analysis (Week 4).** Built a risk register from the vulnerability assessment findings, prioritized by severity, with a remediation roadmap. My Week 5 and Week 6 work builds directly on top of this register.

## Tools

Kali Linux, Nmap, Nikto, NIST National Vulnerability Database.

## A note on scope

In line with the training program's own confidentiality terms, this page stays at the level of method and outcome rather than reproducing raw scan output, lab IP addresses, exact CVE-to-port mappings, or the full original policy/playbook documents verbatim. The Metasploitable 2 target itself is a widely used, publicly documented training VM, freely available for anyone to practice against.

## Note on files previously attached here

Earlier versions of this repo briefly included the original Week 7 and Week 8 documents as attachments. They've been removed. Week 7's original report names a real organization along with specific, unpatched security findings about it; the Week 8 final report and showcase deck consolidate that same material. Neither belongs in a public repo tied to my name — the program's own permission to use this work for LinkedIn and similar doesn't extend to publishing a real institution's unpatched weaknesses, so those two documents are described only at the generic level above.
