# 05 — Alerting and Dashboards (Graylog)

---

## Scenario

After successfully ingesting logs and applying processing pipelines in Graylog, the next objective is to configure alerts and visualize data through dashboards. This module focuses on creating a functional alert condition for specific logs and building a simple dashboard to track log trends in real time.

---

## What I Did

```bash
# Created a new stream for pipeline-processed logs
# Navigated to Alerts > Event Definitions
# Created a new event definition with the following parameters:
# Title: Pipeline Log Alert
# Stream: Selected processed pipeline stream
# Condition Type: Filter & Aggregation
# Search within the last 1 minute, execute every 1 minute
# Condition: Count() > 0 where log message contains specific test string

# Created a notification type: HTTP Callback (tested but not used)

# Switched to Dashboards > Created New Dashboard
# Title: Pipeline Log Monitor
# Created widgets based on search query for the test logs
```

---

## What I Learned

- Graylog's event definitions allow fine-grained alert conditions with flexible scheduling and thresholds.
- Notifications can be sent via multiple channels including Slack, Email, and HTTP — each requiring different setup complexity.
- Dashboards are constructed from saved searches and widgets; they can be used to monitor log patterns and validate pipeline results in real time.
- The HTTP alert notification was attempted, but omitted due to lab scope. Slack was considered but not used.

---

## Why It Matters

Alerting bridges the gap between passive log collection and active monitoring. Being able to define conditions and visualize logs in dashboards is foundational to building a detection and response capability in a SOC environment.

---
