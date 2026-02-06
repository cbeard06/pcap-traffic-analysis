# Malware Traffic Analysis Report

## Lab Overview
- **Source:** malware-traffic-analysis.net
- **PCAP Name:** 2026-01-31-traffic-analysis-exercise.pcap
- **Date Analyzed:** 2/5/26
- **Analyst:** Connor Beard
- **Tools Used:** Wireshark

## Objective
Answer:
1. What is the IP address of the infected Windows client?
2. What is the MAC address of the infected Windows client?
3. What is the host name of the infected Windows client?
4. What is the user account name from the infected Windows client?
5. What is the full name of the user from the user account?
6. What is the domain from 153.92.1[.]49 that triggered the alert for Lumma Stealer?

---
## Background
-- An analyst at a SOC finds a signature hit for "ET MALWARE Lumma Stealer Victim Fingerprinting Activity" that triggered on traffic from 153.92.1[.]49 over TCP port 80. 




## Environment
- Host OS: Windows 11 Home
- Wireshark Version:
- Analysis Type: Passive PCAP Analysis

---

## Initial Observations
- Capture duration:
- Total packets:
- Notable protocols observed:
- Immediate red flags:

---

## Traffic Analysis

### Protocol Breakdown
- **DNS:**  
- **HTTP / HTTPS:**  
- **TCP:**  
- **TLS:**  

---

### Wireshark Filters Used
```text
dns
http
tcp.handshake.type == 1
tls.handshake.type == 1
