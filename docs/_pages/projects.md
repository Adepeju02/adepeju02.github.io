---
title: "Projects"
permalink: /projects/
toc: true
toc_label: "Jump to Project"
toc_icon: "shield-alt"
---

A collection of hands-on cybersecurity projects across security operations, cloud security, penetration testing, digital forensics, and network monitoring. Each write-up follows the problem I was given, what I actually did, what broke and how I fixed it, and the outcome.

---

## Security Operations & SIEM

### ELK Stack Log Pipeline

**Category:** SIEM / Log Analysis  
**Tools:** Elasticsearch · Logstash (JDBC) · Kibana · MySQL · chrony · Linux

**Objective:** Build an end-to-end log pipeline pulling syslog data from a MySQL backend into Elasticsearch for centralized search and visualization.

**What I did:**
- Configured Logstash's JDBC plugin to ingest records from a remote MySQL syslog table into an `all_logs` Elasticsearch index, growing the index to 130K+ documents
- Built Kibana dashboards to visualize sudo (privileged) activity and failed authentication attempts across the environment
- Diagnosed and resolved VM clock skew between hosts using chrony NTP synchronization, which had been breaking timestamp accuracy
- Fixed a stale `jdbc_last_run` state file that was silently skipping new log records
- Corrected a missing Logstash filter block that caused `@timestamp` to map to ingest time rather than actual event time — rebuilt the Kibana index pattern after the fix

**Outcome:** Working end-to-end pipeline from raw MySQL syslog data to searchable, accurately timestamped security dashboards in Kibana.

**Skills demonstrated:** SIEM pipeline design · Timestamp normalization · Multi-host log aggregation · Kibana dashboard development · NTP synchronization

{% include figure image_path="/assets/images/projects/elk-pipeline-placeholder.png" alt="ELK Stack dashboard screenshot" caption="Kibana dashboard showing authentication failures and sudo activity — replace with your screenshot" %}

---

### Centralized Syslog Collection (rsyslog → MySQL)

**Category:** SIEM / Log Analysis  
**Tools:** rsyslog · MySQL · LogAnalyzer · OPNsense · netplan · Linux

**Objective:** Centralize logs from a firewall and multiple hosts into a single MySQL-backed logging server for unified querying.

**What I did:**
- Configured rsyslog on a dedicated log host to receive and store logs forwarded from OPNsense and multiple VMs
- Deployed LogAnalyzer as a web front-end for querying stored log data
- Resolved VirtualBox host-only networking issues and netplan YAML syntax errors blocking cross-host communication
- Fixed MySQL user permissions scoped incorrectly by source IP, preventing remote log insertion
- Diagnosed DNS override conflicts on OPNsense that were breaking the syslog forwarding path

**Outcome:** Functioning centralized logging setup receiving and storing structured logs from multiple network devices and hosts.

**Skills demonstrated:** Centralized log management · Network troubleshooting · Database permission management · Firewall/DNS configuration

{% include figure image_path="/assets/images/projects/rsyslog-placeholder.png" alt="Centralized syslog setup screenshot" caption="LogAnalyzer web interface showing aggregated logs — replace with your screenshot" %}

---

## Cloud Security

### AWS ALB & RDS Troubleshooting

**Category:** Cloud Security / Infrastructure  
**Tools:** AWS (EC2, ALB, RDS/MariaDB, VPC, IAM) · PHP · mysqli · Linux

**Objective:** Diagnose and fix a misconfigured Application Load Balancer and resolve SSL/TLS-enforced database connectivity failures in a live multi-tier web application.

**What I did:**
- Identified that the ALB was configured as internal-facing instead of internet-facing; rebuilt it with correct public subnet associations to restore public traffic routing
- Diagnosed why a PHP application was failing to connect to RDS: MariaDB had `require_secure_transport=ON`, blocking all non-SSL MySQL connections
- Used `--ssl-ca=` flags to complete a data import over SSL, then modified three PHP files (`menu.php`, `processOrder.php`, `orderHistory.php`) to explicitly call `mysqli_ssl_set()` with `MYSQLI_CLIENT_SSL` — enabling the application to connect securely without bypassing the server-side enforcement
- Identified that IAM permissions blocked disabling SSL enforcement at the parameter group level; implemented and documented an application-layer workaround rather than suppressing the graded task

**Outcome:** ALB correctly routing public traffic; PHP application connecting to RDS over enforced TLS with proper SSL context configured at the application layer.

**Skills demonstrated:** AWS networking (VPC, subnets, ALB) · RDS/MySQL TLS configuration · IAM permissions analysis · Application-layer SSL remediation · Cloud troubleshooting methodology

{% include figure image_path="/assets/images/projects/aws-alb-placeholder.png" alt="AWS ALB configuration screenshot" caption="AWS console showing ALB configuration and RDS connectivity — replace with your screenshot" %}

---

## Network Monitoring

### Network Monitoring Stack — SNMP, Traps & NetFlow

**Category:** Network Monitoring  
**Tools:** LibreNMS · SNMPv3 · snmptrapd · Postfix · ntopng · OPNsense · Linux

**Objective:** Deploy a layered monitoring and alerting stack for a home lab network, covering polling, event-driven alerting, and traffic analysis.

**What I did:**
- Configured SNMPv3 on network devices and integrated them with LibreNMS for polling-based device and performance monitoring
- Set up `snmptrapd` to receive SNMP trap events and wired it to Postfix for automated email alerting on network events
- Deployed ntopng for NetFlow-based traffic analysis and bandwidth visibility
- Resolved an OS/package version incompatibility on Ubuntu that blocked the standard ntopng installation by sourcing the package from ntop's alternate repository

**Outcome:** A layered monitoring stack providing continuous polling (LibreNMS), event-driven alerting (SNMP traps + email), and real-time traffic visibility (NetFlow/ntopng).

**Skills demonstrated:** SNMPv3 · Network monitoring · SNMP trap configuration · Email alerting integration · NetFlow traffic analysis · Package management troubleshooting

{% include figure image_path="/assets/images/projects/librenms-placeholder.png" alt="LibreNMS dashboard screenshot" caption="LibreNMS polling dashboard with device status — replace with your screenshot" %}

---

## Home Lab & Infrastructure

### Home Lab Server Setup

**Category:** Infrastructure / Security Lab  
**Tools:** Linux (Ubuntu/Debian) · VirtualBox · Networking · Various security tools

**What I built:**
- Provisioned and maintained a multi-VM home lab environment to practice hands-on security skills
- Configured host-only and NAT networking across VMs to simulate isolated network segments
- Used the lab as the foundation for the ELK Stack, rsyslog, network monitoring, and penetration testing projects documented above
- Maintained documentation of configurations, issues encountered, and resolutions — developing a habit of treating the lab like a production environment

**Skills demonstrated:** Linux system administration · VM networking · Lab documentation · Infrastructure-as-practice methodology

---

## Digital Forensics

### Microsoft Filesystem Forensic Analysis

**Category:** Digital Forensics  
**Tools:** Autopsy · ProDiscover Basic · AccessData Registry Viewer · Tsurugi Linux · VirtualBox

**Objective:** Conduct four separate forensic investigations on Windows disk images to recover evidence and establish evidentiary links between files, users, and events.

**What I did:**
- Used Autopsy and ProDiscover to examine disk images, recovering deleted photo evidence from the Windows Recycle Bin and identifying files linking two individuals
- Located Zone.Identifier Alternate Data Streams (ADS) indicating files had been downloaded from the internet — used as digital evidence of origin
- Used AccessData Registry Viewer to trace Outlook Express artifacts and registry entries connecting a suspect employee to an external party
- Adapted the VMware-based lab to run on VirtualBox, including disabling BitLocker (`manage-bde -off C:`) on a Windows 11 evidence target to enable imaging

**Outcome:** All four investigations completed with documented evidence chains, demonstrating the ability to recover, correlate, and present digital artifacts from Windows environments.

**Skills demonstrated:** Disk image forensics · Deleted file recovery · Alternate Data Streams · Registry artifact analysis · Email artifact tracing · Chain of custody documentation

{% include figure image_path="/assets/images/projects/forensics-placeholder.png" alt="Autopsy forensic investigation screenshot" caption="Autopsy showing recovered evidence artifacts — replace with your screenshot" %}

---

## Penetration Testing

### Password & Hash Cracking

**Category:** Penetration Testing / Credential Security  
**Tools:** Kali Linux · Hashcat · John the Ripper · Metasploit (EternalBlue) · Metasploitable3

**Objective:** Practice credential attack techniques across multiple methods, from benchmarking to real exploit-based credential extraction.

**What I did:**
- Benchmarked Hashcat GPU/CPU performance, then executed dictionary and mask attacks to crack NTLM hashes
- Used John the Ripper with explicit `--format=Raw-MD5` flag after diagnosing that auto-detection was silently failing to identify the hash format
- Exploited Metasploitable3 using the EternalBlue (MS17-010) SMB vulnerability via Metasploit to gain access and dump password hashes from memory

**Outcome:** Hashes successfully cracked via dictionary, mask, and format-specific methods; credential extraction demonstrated through a real exploit chain against a vulnerable target.

**Skills demonstrated:** Hash cracking methodologies · Metasploit exploitation · SMB vulnerability analysis · Credential security · Offensive security techniques

{% include figure image_path="/assets/images/projects/hashcracking-placeholder.png" alt="Hashcat cracking session screenshot" caption="Hashcat session cracking NTLM hashes — replace with your screenshot" %}

---

### Recon & Exploitation (Metasploit / OSINT)

**Category:** Penetration Testing / Reconnaissance  
**Tools:** Kali Linux · Metasploit · Nmap · theHarvester · Sublist3r · Google Dorking

**Objective:** Practice enumeration, exploitation, and OSINT-based reconnaissance against isolated lab targets.

**What I did:**
- Ran Nmap enumeration against lab VMs to map open ports, services, and OS fingerprints before exploitation
- Executed Metasploit exploitation against lab targets, including an Elasticsearch Remote Code Execution (RCE) exploit
- Conducted OSINT reconnaissance using theHarvester and Sublist3r for subdomain and email enumeration; adapted to online OSINT alternatives when the lab's NAT-only networking blocked the sandboxed tools from reaching the internet
- Applied Google Dorking techniques to surface publicly exposed information about target organizations

**Outcome:** Completed enumeration and exploitation objectives against all targets; adapted OSINT methodology around a real network constraint rather than skipping the requirement.

**Skills demonstrated:** Network enumeration · Metasploit exploitation · RCE vulnerability abuse · OSINT methodology · Google Dorking · Adaptive problem-solving under constraints

{% include figure image_path="/assets/images/projects/recon-placeholder.png" alt="Nmap and Metasploit session screenshot" caption="Nmap enumeration and Metasploit exploitation output — replace with your screenshot" %}

---

## Work Experience Projects

### Township of Spring Water — IT Security Initiatives

**Role:** IT Student (Cybersecurity Focus)  
**Tools:** Wazuh · Fortinet · Microsoft Entra ID · Microsoft Intune · KnowBe4 · Microsoft Excel · Microsoft 365 · Windows · Linux

The following reflects hands-on work completed during my placement at the Township of Spring Water. Specific metrics are noted where recordable; placeholders marked `[X]` represent figures to be added.

**Cybersecurity, Risk & Governance**

- Deployed Wazuh SIEM from scratch on Linux, onboarding `[X]` endpoints and log sources for centralized monitoring and threat visibility across the organization
- Configured Fortinet firewall policies and settings, implementing `[X]` rule changes to strengthen network segmentation and access control
- Built and maintained an IT risk register in Microsoft Excel, documenting `[X]` identified risks across `[X]` categories and supporting prioritization and mitigation planning
- Updated the organization's Acceptable Use Policy (AUP) in Microsoft Word, revising `[X]` sections to improve clarity and align with current security standards
- Created and managed `[X]` phishing simulation campaigns in KnowBe4, supporting staff cybersecurity awareness and phishing-readiness measurement

**Identity & Access Management**

- Resolved `[X]` user permission and access issues using Microsoft Entra ID, improving access reliability and reducing resolution delays for staff

**IT Operations & Device Deployment**

- Deployed `[X]` laptops, phones, and workstations using Windows and Microsoft 365, supporting staff onboarding and device replacement
- Set up workstations from scratch — imaging, account setup, software installation, and peripheral configuration — for `[X]` users
- Supported Microsoft Intune MDM administration, managing `[X]` enrolled devices for compliance policy enforcement and secure access
