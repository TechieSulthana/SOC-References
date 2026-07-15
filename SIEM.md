# SOC Analyst Reference: SIEM Operations (Splunk Processing Language)

## Executive Summary
This section outlines core Security Information and Event Management (SIEM) operations using Splunk Processing Language (SPL). It establishes baseline logic for filtering massive enterprise log repositories (`indices`), transforming raw strings into structured metrics, and tracking active malicious indicators.

---

## 1. Splunk Search Anatomy
Every ingested log contains essential metadata fields utilized to optimize query performance and reduce resource load:
* `index`: Controls the logical data partition (e.g., `index=security`, `index=network`).
* `sourcetype`: Identifies the system format (e.g., `WinEventLog:Security`, `cisco_vpn`, `linux_secure`).
* `host`: Identifies the target hardware asset generating the telemetry data.

---

## 2. Core Operational SPL Commands (Tier 1 Triage)

### A. Data Structuring (`table`)
Raw text logs are converted into legible, sequential grids prioritizing analytical variables:
```splunk
index=security EventCode=4625 | table _time, host, User, src_ip
