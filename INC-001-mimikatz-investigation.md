* INC-001 — Mimikatz Credential Dump Investigation

## Summary
Investigated a real-world style attack dataset (OTRF Security Datasets)
involving PowerShell Empire C2, Mimikatz LSASS credential dumping,
and Pass-the-Hash lateral movement to a Domain Controller.

* Environment
- Tool used: Splunk Free (local install)
- Dataset: OTRF empire_mimikatz_logonpasswords
- Date of analysis: June 2026

* Attack Timeline
| Time     | Event                                      |
|----------|--------------------------------------------|
| 10:32:02 | PowerShell C2 beacon to 10.10.10.5:80      |
| 10:32:02 | LSASS/AD enumeration via port 389          |
| 10:32:56 | Mimikatz dumps LSASS (GrantedAccess 0x478) |
| 10:32-34 | 10x Pass-the-Hash logins to MORDORDC$      |

* IOCs
| Type             | Value                        |
|------------------|------------------------------|
| C2 Server        | 10.10.10.5 (port 80)         |
| Attacker process | powershell.exe PID 1648      |
| Compromised host | WORKSTATION5.theshire.local  |
| Domain Controller| 172.18.38.5                  |
| Malware signature| GrantedAccess 0x478          |

* MITRE ATT&CK
- T1059.001 — PowerShell
- T1003.001 — LSASS Memory dump
- T1550.002 — Pass-the-Hash
- T1021.002 — Lateral movement SMB
- T1071.001 — C2 over HTTP

* Splunk Queries Used
1.index=main EventID=10 | table _time, SourceImage, TargetImage, GrantedAccess
2.index=main EventID=10
| table _time, SourceImage, TargetImage, GrantedAccess, Hostname
| sort _time
3.index=main EventID=1 ProcessId=1648
| table _time, Image, CommandLine, ParentImage, ParentCommandLine, User
4.index=main EventID=3
| table _time, Image, DestinationIp, DestinationPort, DestinationHostname
| sort _time

* Conclusion
Full domain compromise confirmed. Attacker used
PowerShell Empire for C2, Mimikatz for credential
theft, and Pass-the-Hash to reach the Domain
Controller within 2 minutes of initial access.