# 01 — Splunk Log Ingest

---

## Scenario

I needed to test whether a custom log file could be ingested by Splunk and correctly parsed into searchable events. My goal was to simulate a Suricata-style alert and validate the end-to-end ingestion pipeline.

---

## What I Did

```bash
# Created a sample log file
cat > ~/sample_suricata.log <<EOF
{"timestamp":"2025-07-31T12:00:00.000Z","event_type":"alert","src_ip":"192.168.1.22","dest_ip":"93.184.216.34","alert":{"signature":"ET TROJAN Downloader","category":"A Network Trojan was detected"}}
EOF
```

- Switched to running Splunk on my native Windows OS due to VM disk issues
- Used Splunk Web to manually upload `sample_suricata.log`
- Selected `sourcetype = _json` during ingestion
- Verified successful event parsing via Splunk Search

---

## What I Learned

- Splunk is capable of ingesting structured JSON logs and automatically extracting fields like `src_ip`, `dest_ip`, `event_type`, and `timestamp`
- Even a single line of well-formatted JSON can be parsed and visualized effectively
- Disk space limitations on a VM can prevent Splunk from functioning; moving to a native OS helped bypass this

---

## Why It Matters

Simulating a real-world Suricata log ingestion validates my ability to:

- Handle ingestion of structured network alerts
- Use Splunk’s field extraction and search features
- Troubleshoot Splunk deployment across environments (VM vs native)

---
