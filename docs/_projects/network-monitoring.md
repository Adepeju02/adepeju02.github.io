---
title: "Network Monitoring Stack — SNMP, Traps & NetFlow"
category: "Network Monitoring"
tools: "LibreNMS · SNMPv3 · snmptrapd · Postfix · ntopng · OPNsense · Linux"
excerpt: "Built a layered home-lab monitoring stack covering polling (LibreNMS), event-driven alerting (SNMP traps + email), and traffic visibility (NetFlow/ntopng)."
header:
  teaser: /assets/images/projects/librenms-placeholder.png
---

**Category:** Network Monitoring  
**Tools:** LibreNMS · SNMPv3 · snmptrapd · Postfix · ntopng · OPNsense · Linux

---

## Objective

Deploy a layered monitoring and alerting stack for a home lab network, covering polling, event-driven alerting, and traffic analysis.

## What I Did

- Configured SNMPv3 on network devices and integrated them with LibreNMS for polling-based device health and performance monitoring
- Set up `snmptrapd` to receive SNMP trap events and wired it to Postfix for automated email alerting on network events
- Deployed ntopng for NetFlow-based traffic analysis and real-time bandwidth visibility across the lab network

## Challenges & How I Solved Them

- **Package compatibility:** Ubuntu had an OS/package version mismatch that blocked the standard ntopng installation from the default repo — resolved by sourcing the package from ntop's alternate (unstable) repository and verifying the install

## Outcome

A layered monitoring stack providing continuous polling (LibreNMS), event-driven alerting (SNMP traps + email), and real-time traffic visibility (NetFlow/ntopng) across the home lab.

## Skills Demonstrated

SNMPv3 configuration · LibreNMS deployment · SNMP trap alerting · Postfix email integration · NetFlow traffic analysis · ntopng · Package management troubleshooting · Network monitoring architecture

{% include figure image_path="/assets/images/projects/librenms-placeholder.png" alt="LibreNMS polling dashboard" caption="LibreNMS device polling dashboard — replace with your screenshot" %}
