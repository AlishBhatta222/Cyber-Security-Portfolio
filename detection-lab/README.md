
# Project 2: Sigma Detection Rules with Splunk Validation
Detection Lab: Sigma Rules
Detection as code for a home SOC lab. Every rule here was written in Sigma, converted to Splunk SPL automatically, and validated by firing it against real telemetry in my own Splunk instance. Nothing in this repo is theory only.
This project demonstrates a basic detection engineering workflow using Sigma rules and Splunk to detect Windows authentication activity, including repeated failed logons and successful logons after brute-force attempts.

## Objective

The goal of this project was to create and validate Sigma-based detection logic for Windows logon events. The lab focuses on identifying suspicious authentication behaviour such as multiple failed logon attempts from the same source, followed by a successful login.

This type of activity can indicate password spraying, brute-force attempts, credential guessing, or unauthorized access attempts.

## What This Lab Covers

- Windows authentication log analysis
- Failed logon detection
- Successful logon monitoring
- Sigma rule creation
- Splunk search validation
- Detection pipeline structure
- Evidence collection through screenshots

## Tools Used

- Windows Event Logs
- Splunk
- Sigma rules
- Kali Linux
- SMB authentication testing
- GitHub for documentation and portfolio evidence

## Repository Structure

```text
detection-lab/
│
├── pipelines/
│   └── Detection pipeline files
│
├── rules/
│   └── Sigma detection rules
│
├── Failed logons.png
├── Failed logons by source.png
├── Successful logons.png
└── README.md
