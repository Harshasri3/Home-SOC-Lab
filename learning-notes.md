# Learning Notes

This document summarizes the key concepts and practical knowledge gained while building the Home SOC Lab.

---

## Splunk

* Installed and configured Splunk Enterprise.
* Learned how Splunk indexes and searches log data.
* Explored the Search & Reporting application.
* Used SPL to search, filter, and analyze Windows logs.

---

## Universal Forwarder

* Installed the Splunk Universal Forwarder.
* Configured the forwarder to send Windows Event Logs to Splunk.
* Verified successful communication using receiving port 9997.

---

## Sysmon

* Installed Sysmon using a community configuration file.
* Verified Sysmon event generation.
* Collected detailed endpoint telemetry including process creation and network connections.

---

## Windows Event Logs

Learned the difference between standard Windows Event Logs and Sysmon events.

Examples of monitored events:

* Process Creation (Event ID 1)
* Network Connections (Event ID 3)
* DNS Queries (Event ID 22)

---

## SPL Queries

Practiced writing queries to:

* Search specific Event IDs
* Filter events
* Display selected fields
* Count occurrences
* Sort events by time
* Summarize endpoint activity

Common SPL commands used:

* search
* table
* stats
* sort

---

## Endpoint Analysis

Performed analysis on:

* Newly created processes
* Interactive PowerShell execution
* Outbound network connections
* Parent-child process relationships
* Frequently executed applications

---

## Key Takeaways

* Windows endpoints generate valuable security telemetry.
* Sysmon provides significantly more visibility than default Windows logging.
* SPL enables efficient searching and investigation of large log datasets.
* Understanding process behavior and network activity is essential for SOC analysts.
* Organizing investigations with repeatable SPL queries improves analysis efficiency.



---

This document will continue to be updated as additional tools, log sources, and detection techniques are explored.
