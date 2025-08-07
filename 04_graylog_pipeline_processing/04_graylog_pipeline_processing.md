# 04 — Pipeline Processing

---

## Scenario

After successfully routing logs to a custom stream using Graylog's `udp` input, the next step was to enrich and structure the logs using pipeline rules. This module focused on extracting fields such as log level, message content, and timestamp from a plain-text UDP log and routing the result through a functional pipeline.

---

## What I Did

```bash
# 1. Sent test log via UDP
echo "2025-08-07 21:30:00 INFO Test log from Graylog pipeline lab" | nc -u localhost 5555
```

1. Created a custom stream named `udp-test-stream`.
2. Added a **stream rule** using a regular expression to match `message` containing `"Graylog pipeline lab"`.
3. Built a **pipeline** with the following rules:
   - Extracted `timestamp`, `log_level`, and `message` using regex.
   - Converted timestamp to proper Graylog format.
4. Connected the pipeline to the `udp-test-stream`.
5. Verified that:
   - The message was routed correctly.
   - Fields `log_level`, `timestamp`, `message`, and `source` were extracted.
   - The document showed up in both the stream and search views with parsed fields.

---

## What I Learned

- Graylog pipelines can parse, modify, and route log messages dynamically at ingestion time.
- Regular expressions in pipeline rules allow for precise field extraction from raw log data.
- Stream rules work best when kept simple (e.g., regex matches) and used in combination with pipelines for more complex processing.
- The `Set field` and `Parse date` functions are essential for transforming raw text into structured fields usable in dashboards or alerts.

---

## Why It Matters

Without pipelines, incoming logs would remain unstructured text, making queries and alerts unreliable. Pipeline processing enables consistent enrichment of logs, turning flat messages into structured documents. This is foundational for building dashboards, performing searches, and detecting threats using log-level context and parsed metadata. 

---
