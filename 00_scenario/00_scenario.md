# 00 — Scenario

---

## Scenario

You are a newly onboarded SOC Tier 1 analyst at a mid-sized enterprise. The organization uses both **Splunk** and **Graylog** to aggregate logs from various sources across its Windows and Linux infrastructure. Your role in this lab is to demonstrate your ability to ingest, normalize, and correlate log data across platforms, then build detections that highlight suspicious or anomalous activity.

This lab simulates core SIEM workflows including ingestion, parsing, dashboard creation, and detection rule authoring — with a focus on *practical implementation* over threat emulation.

---

## Objective

- Configure and verify log ingestion into both Splunk and Graylog
- Analyze and normalize logs from sources such as Sysmon, Suricata, or web servers
- Build correlation rules or searches that surface meaningful security signals
- Compare how each SIEM handles the same data
- Document detections using visualizations and structured markdown

---

## Lab Environment

| Component     | Platform            |
|---------------|---------------------|
| Splunk Free   | Installed locally or via Docker |
| Graylog       | Docker-based or VM deployment   |
| Log Sources   | Sysmon, Suricata, custom JSON/web logs |

---

## Threat Simulation Summary

This lab does **not** focus on attacker simulation. Instead, it emphasizes core SOC workflows:
- Ingesting high-volume data
- Making that data actionable
- Surfacing security-relevant insights across platforms

---

## Blue Team Focus

- Data normalization and field mapping
- Splunk vs Graylog correlation methods
- SIEM query logic and tuning
- Custom detection writing and alerting

---

## Disclaimer

This lab is designed for educational and defensive skill-building purposes only. All systems are isolated in a virtual lab environment and simulate benign or anonymized data. No actual malicious activity is performed or encouraged.

---
