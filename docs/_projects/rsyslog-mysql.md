---
title: "Centralized Syslog Collection"
category: "SIEM / Log Analysis"
tools: "rsyslog · MySQL · LogAnalyzer · OPNsense · netplan · Linux"
excerpt: "Centralized logs from a firewall and multiple VMs into a single MySQL-backed logging server, resolving networking, DNS, and permission issues along the way."
header:
  teaser: /assets/images/projects/rsyslog-placeholder.png
---

**Category:** SIEM / Log Analysis  
**Tools:** rsyslog · MySQL · LogAnalyzer · OPNsense · netplan · Linux

---

## Objective

Centralize logs from a firewall and multiple hosts into a single MySQL-backed logging server for unified querying and review.

## What I Did

- Configured rsyslog on a dedicated log host to receive and store logs forwarded from OPNsense and multiple VMs
- Deployed LogAnalyzer as a web front-end for querying stored log data across all sources

## Challenges & How I Solved Them

- **VirtualBox networking:** Host-only network adapter issues prevented cross-VM communication — diagnosed and corrected adapter configuration
- **netplan YAML errors:** Syntax errors in netplan configuration blocked network bring-up — validated and corrected the YAML structure
- **MySQL permissions:** User permissions were scoped by source IP and rejected remote log insertion — updated grants to allow the correct host ranges
- **OPNsense DNS conflicts:** DNS override settings on OPNsense were intercepting the syslog forwarding path — identified the conflict and adjusted DNS resolution order

## Outcome

Functioning centralized logging setup receiving and storing structured logs from multiple network devices and hosts, queryable through a web interface.

## Skills Demonstrated

Centralized log management · rsyslog configuration · MySQL administration · OPNsense/firewall DNS · Network troubleshooting · LogAnalyzer deployment

{% include figure image_path="/assets/images/projects/rsyslog-placeholder.png" alt="Centralized syslog LogAnalyzer interface" caption="LogAnalyzer web interface showing aggregated logs — replace with your screenshot" %}
