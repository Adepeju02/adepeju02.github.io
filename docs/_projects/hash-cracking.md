---
title: "Password & Hash Cracking"
category: "Penetration Testing"
tools: "Kali Linux · Hashcat · John the Ripper · Metasploit (EternalBlue) · Metasploitable3"
excerpt: "Practiced credential attack techniques across dictionary, mask, and format-specific methods, then extracted hashes from a vulnerable target via the EternalBlue exploit chain."
header:
  teaser: /assets/images/projects/hashcracking-placeholder.png
---

**Category:** Penetration Testing / Credential Security  
**Tools:** Kali Linux · Hashcat · John the Ripper · Metasploit (EternalBlue) · Metasploitable3

---

## Objective

Practice credential attack techniques across multiple methods — from benchmarking to real exploit-based hash extraction.

## What I Did

- Benchmarked Hashcat GPU/CPU performance to understand attack speed baselines
- Executed dictionary and mask attacks using Hashcat to crack NTLM hashes
- Used John the Ripper with explicit `--format=Raw-MD5` flag after diagnosing that auto-detection was silently failing on the hash format
- Exploited Metasploitable3 using the EternalBlue (MS17-010) SMB vulnerability via Metasploit to gain access and dump password hashes from memory

## Challenges & How I Solved Them

- **John the Ripper format detection failure:** Auto-detection silently failed to identify the hash format, causing John to run with the wrong algorithm and produce no results. Diagnosed by examining the hash string manually and passing `--format=Raw-MD5` explicitly — a reminder that tool defaults aren't always reliable.

## Outcome

Hashes cracked successfully via dictionary, mask, and format-specific attack methods; credentials extracted through a real EternalBlue exploit chain against Metasploitable3.

## Skills Demonstrated

Hash cracking methodologies (dictionary, mask, format-specific) · Hashcat · John the Ripper · Metasploit exploitation · EternalBlue / MS17-010 · SMB vulnerability analysis · Credential security

{% include figure image_path="/assets/images/projects/hashcracking-placeholder.png" alt="Hashcat cracking session" caption="Hashcat session showing cracked NTLM hashes — replace with your screenshot" %}
