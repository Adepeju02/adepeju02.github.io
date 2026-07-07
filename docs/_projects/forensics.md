---
title: "Microsoft Filesystem Forensic Analysis"
category: "Digital Forensics"
tools: "Autopsy · ProDiscover Basic · AccessData Registry Viewer · Tsurugi Linux · VirtualBox"
excerpt: "Conducted four separate forensic investigations on Windows disk images, recovering deleted evidence and tracing registry and email artifacts to establish evidentiary links between suspects."
header:
  teaser: /assets/images/projects/forensics-placeholder.png
---

**Category:** Digital Forensics  
**Tools:** Autopsy · ProDiscover Basic · AccessData Registry Viewer · Tsurugi Linux · VirtualBox

---

## Objective

Conduct four separate forensic investigations on Windows disk images to recover evidence and establish links between files, users, and events.

## What I Did

- Used Autopsy and ProDiscover to examine disk images, recovering deleted photo evidence from the Windows Recycle Bin and identifying files linking two individuals
- Located Zone.Identifier Alternate Data Streams (ADS) on recovered files, indicating they had been downloaded from the internet — establishing digital provenance as evidence
- Used AccessData Registry Viewer to trace Outlook Express artifacts and registry entries connecting a suspect employee to an external party
- Adapted a VMware-based lab environment to run on VirtualBox, including disabling BitLocker (`manage-bde -off C:`) on a Windows 11 evidence target to enable disk imaging

## Challenges & How I Solved Them

- **BitLocker on evidence drive:** The Windows 11 target had BitLocker enabled, blocking imaging. Disabled it using `manage-bde -off C:` before proceeding — and documented the step to maintain chain of custody transparency.
- **VMware → VirtualBox adaptation:** The lab was written for VMware; adapted VM settings, network adapters, and disk attachment methods to work within VirtualBox without compromising the investigation environment.

## Outcome

All four investigations completed with documented evidence chains demonstrating ability to recover, correlate, and present digital artifacts from Windows environments using industry-standard forensic tools.

## Skills Demonstrated

Disk image forensics · Deleted file recovery · Alternate Data Streams (ADS) analysis · Windows Registry artifact analysis · Email artifact tracing (Outlook Express) · Chain of custody documentation · Cross-platform lab adaptation

{% include figure image_path="/assets/images/projects/forensics-placeholder.png" alt="Autopsy forensic investigation interface" caption="Autopsy showing recovered evidence artifacts — replace with your screenshot" %}
