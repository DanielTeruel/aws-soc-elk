# 04 — Kibana Index Pattern + Discover

## Overview

Create an index pattern in Kibana to expose the Logstash indices for exploration, then use the Discover view to query and visualize the ingested events with full field breakdown.

---

## Step 1 — Create Index Pattern

![Stack Management](../screenshots/26.png)

Navigate to **Kibana → Stack Management → Index Patterns**.

![Index Pattern Config](../screenshots/27.png)

Create an index pattern targeting `logstash*`:

| Setting | Value |
|---|---|
| Pattern | `logstash*` |
| Matches | All Logstash indices regardless of date suffix |
| Time field | `@timestamp` |

The wildcard `*` ensures the pattern matches all current and future Logstash indices automatically.

![Index Pattern Fields](../screenshots/28.png)

Kibana discovers all fields present in the matching indices — message, host, @timestamp, Logstash tags and any custom fields added by filters.

---

## Step 2 — Explore Data in Discover

![Discover Final](../screenshots/29.png)

All ingested Logstash events are now visible in **Kibana → Discover** with:

- Full field breakdown in the left panel
- Timeline histogram showing event distribution
- Expandable event rows with all metadata
- Filter and search capabilities across all fields

| Field | Value |
|---|---|
| message | Test message typed via stdin |
| host | elk (container hostname) |
| @timestamp | Ingestion time |
| tags | _jsonparsefailure (expected for plain text input) |

---

## Key Concepts

| Concept | Description |
|---|---|
| Index Pattern | Kibana abstraction over one or more Elasticsearch indices |
| `logstash*` wildcard | Matches all indices created by Logstash regardless of date |
| @timestamp | Default time field used for histogram and time filtering |
| Discover | Kibana tool for ad-hoc log exploration and field analysis |
