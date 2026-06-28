# Splunk Analysis Examples

This document demonstrates how Splunk was used to analyze Windows endpoint activity collected through Sysmon. Each example includes the objective, SPL query, analysis performed, and findings.

---

# Analysis 1 – Process Creation

## Objective

Review recently created processes on the Windows endpoint.

## SPL Query

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
| table _time Image CommandLine ParentImage User
| sort -_time
```

## Analysis

- Reviewed recently executed processes.
- Verified executable paths and command-line arguments.
- Examined parent-child process relationships.
- Confirmed the associated user account.

## Findings

Normal process execution was observed, including Windows applications, Visual Studio Code, Google Chrome, and administrative tools. No suspicious process execution or abnormal parent-child relationships were identified.

---

# Analysis 2 – PowerShell Execution

## Objective

Analyze interactive PowerShell execution.

## SPL Query

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
Image="*\\WindowsPowerShell\\v1.0\\powershell.exe"
| table _time Image CommandLine ParentImage User
| sort -_time
```

## Analysis

- Identified PowerShell execution initiated by the logged-in user.
- Reviewed the process path and integrity level.
- Verified the parent process and command line.

## Findings

PowerShell was launched interactively to execute administrative commands (`whoami`, `hostname`, `ipconfig`, `Get-Date`, and `Get-Process`) during lab testing. No encoded commands or suspicious execution patterns were observed.

---

# Analysis 3 – Network Connections

## Objective

Review outbound network connections initiated by endpoint processes.

## SPL Query

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=3
| stats count by Image DestinationIp DestinationPort Protocol
| sort -count
```

## Analysis

- Reviewed outbound connections grouped by process.
- Identified the destination IP addresses and ports.
- Verified the communication protocol.

## Findings

Visual Studio Code, Microsoft Office applications, and Google Chrome generated outbound HTTPS connections over TCP port 443. DNS requests over UDP port 53 were also observed. No unexpected ports or suspicious destinations were identified.

---

# Analysis 4 – Parent-Child Process Relationships

## Objective

Review parent-child process relationships to understand process execution flow.

## SPL Query

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
| table _time ParentImage Image CommandLine User
| sort -_time
```

## Analysis

- Verified which parent processes launched child processes.
- Reviewed command-line arguments.
- Checked the user context.

## Findings

Observed expected parent-child relationships such as `explorer.exe` launching user applications. No unusual process chains indicative of malicious activity were identified.