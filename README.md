# SOC Investigation Reports

Hands-on incident response investigations using real 
attack datasets, Splunk, and Wireshark. Each report 
follows a real SOC analyst workflow — triage, 
investigation, IOC extraction, MITRE ATT&CK mapping, 
and formal incident writeup.

---

## Investigations completed

| # | Incident | Attack Type | Tool | Severity |
|---|----------|-------------|------|----------|
| 1 | [INC-001 — Mimikatz Credential Dump](./INC-001-mimikatz-investigation.md) | LSASS dump → Pass-the-Hash → DC compromise | Splunk | P1 Critical |
| 2 | INC-002 — Phishing Analysis | Coming soon | PhishTool / MXToolbox | - |
| 3 | INC-003 — C2 Beacon Detection | Coming soon | Wireshark | - |

---

## Skills demonstrated
- Splunk SPL querying and log analysis
- Windows Event ID investigation (4624, 4625, EventID 10)
- MITRE ATT&CK technique mapping
- IOC extraction and defanging
- Incident report writing

---

## Tools used
Splunk Free · Wireshark · MITRE ATT&CK Navigator · 
VirusTotal · MXToolbox · URLScan.io · Any.run

---

## Dataset sources
- [OTRF Security Datasets](https://github.com/OTRF/Security-Datasets)
- [Malware Traffic Analysis](https://malware-traffic-analysis.net)
