# 02 — Detection Logic

---

## Scenario

The task was to validate that Splunk could search and correlate fields from an uploaded Suricata log. This involved crafting detection logic to identify alerts based on key fields within the JSON structure of the event.

---

## What I Did

```spl
# Verified event was searchable
index=main

# Attempted field-level search for Suricata alert
index=main event_type=alert signature="ET TROJAN Downloader"
# (No results — likely due to unparsed nested JSON structure)

# Performed raw string search to confirm ingestion
index=main _raw="{\"timestamp\":\"2025-07-31T12:00:00.000Z\",\"event_type\":\"alert\",\"src_ip\":\"192.168.1.22\",\"dest_ip\":\"93.184.216.34\",\"alert\":{\"signature\":\"ET TROJAN Downloader\",\"category\":\"A Network Trojan was detected\"}}"
# (Search successful — matched exact JSON)
```

---

## What I Learned

- Field-level detection failed due to the lack of automatic parsing for nested JSON fields.
- Raw event search confirmed that the log was ingested correctly.
- Splunk requires custom field extractions to query nested fields from Suricata-style logs.
- Basic detection is possible, but not scalable without improved parsing.

---

## Why It Matters

Detection logic depends on structured, searchable fields. This test revealed how JSON field handling impacts Splunk's ability to detect meaningful alerts from tools like Suricata. Effective detection engineering must account for log format and ingestion behavior to support reliable correlation logic.

---
