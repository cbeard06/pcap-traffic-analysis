# Malware Traffic Analysis Report

## Lab Overview
- **Source:** malware-traffic-analysis.net
- **PCAP Name:**
- **Date Analyzed:**
- **Analyst:** Connor Beard
- **Tools Used:** Wireshark

## Objective
Analyze the provided PCAP file to identify malicious network activity and extract
relevant indicators of compromise (IOCs).

---

## Background




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
