# Splunk SOC Detection Lab: Attack Chain Simulation and Hunting

## Overview

This project is Part 2 of my SOC Analyst Home Lab series. After building a working detection lab and confirming telemetry into Splunk, I simulated a realistic attack chain and hunted each stage using Splunk.

The lab followed a practical intrusion flow:

1. Reconnaissance  
2. Credential access  
3. Valid credential use  
4. Post-compromise discovery  
5. Suspicious PowerShell execution  

Each stage was mapped to MITRE ATT&CK to show how raw logs can be turned into analyst-level detections.

## Lab Environment

- Kali Linux as the attacker machine
- Windows 11 as the victim endpoint
- Sysmon with SwiftOnSecurity configuration
- Splunk Universal Forwarder on the victim
- Ubuntu Server running Splunk Enterprise
- VMware NAT networking

## Attack Chain Simulated

### 1. Reconnaissance

Nmap was used from Kali to scan the Windows victim host.

Tools used:

- `nmap -sn`
- `nmap -sS -p-`
- `nmap -sV -sC`

The scan identified port `7680/tcp`, related to Windows Delivery Optimisation.

### 2. Credential Access

A test local user account was created on the victim machine. A small custom wordlist was used to simulate brute-force activity.

Tools used:

- NetExec against SMB
- Hydra against RDP

The SMB brute-force attempt successfully validated credentials. The RDP attempt failed because the victim was running Windows 11 Home, which does not include an RDP server.

### 3. Splunk Detection: Failed and Successful Logons

Failed authentication attempts were detected using Windows Security Event ID `4625`.

Successful network logon activity was detected using Event ID `4624` with Logon Type `3`.

This showed the classic brute-force pattern:

- Multiple failed logons from one source
- Followed by a successful logon from the same source

### 4. Post-Compromise Discovery

A realistic discovery sequence was executed on the victim host:

```cmd
whoami /priv
net user
net localgroup administrators
ipconfig /all
systeminfo
