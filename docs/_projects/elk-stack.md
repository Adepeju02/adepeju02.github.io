---
title: "ELK Stack Log Pipeline"
category: "SIEM / Log Analysis"
tools: "Elasticsearch · Logstash (JDBC) · Kibana · MySQL · chrony · Linux"
excerpt: "Built an end-to-end log pipeline ingesting 130K+ records from a remote MySQL database into Elasticsearch, with Kibana dashboards for authentication and privilege monitoring."
header:
  teaser: /assets/images/projects/elk-pipeline-placeholder.png
---

**Category:** SIEM / Log Analysis  
**Tools:** Elasticsearch · Logstash (JDBC) · Kibana · MySQL · chrony · Linux

---

## Objective

Build an end-to-end log pipeline pulling syslog data from a MySQL backend into Elasticsearch for centralized search and visualization.

## What I Did

- Configured Logstash's JDBC plugin to ingest records from a remote MySQL syslog table into an `all_logs` Elasticsearch index, growing the dataset to 130K+ documents
- Built Kibana dashboards to visualize sudo (privileged) activity and failed authentication attempts across the environment

## Challenges & How I Solved Them

- **Clock skew:** VM timestamp mismatches between hosts broke log accuracy — resolved with chrony NTP synchronization
- **Stale state file:** Logstash's `jdbc_last_run` file was tracking old timestamps and silently skipping new records — cleared and reconfigured the tracking state
- **Wrong timestamp mapping:** A missing Logstash filter block caused `@timestamp` to reflect ingest time rather than actual event time — added the correct filter and rebuilt the Kibana index pattern after the fix

## Outcome

Working end-to-end pipeline from raw MySQL syslog data to searchable, accurately timestamped security dashboards in Kibana.

## Skills Demonstrated

SIEM pipeline design · Timestamp normalization · Multi-host log aggregation · Kibana dashboard development · NTP synchronization · Logstash JDBC configuration

{% include figure image_path="/assets/images/projects/elk-pipeline-placeholder.png" alt="ELK Stack Kibana dashboard" caption="Kibana dashboard showing authentication failures and sudo activity — replace with your screenshot" %}
