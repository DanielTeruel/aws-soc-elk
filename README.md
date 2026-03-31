![SOC Lab Banner](./banner.png)

# SOC Lab — ELK Stack on AWS

![AWS](https://img.shields.io/badge/AWS-EC2-FF9900?style=flat&logo=amazonaws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-7.16.3-005571?style=flat&logo=elasticsearch&logoColor=white)
![Logstash](https://img.shields.io/badge/Logstash-7.16.3-FEC514?style=flat&logo=logstash&logoColor=black)
![Kibana](https://img.shields.io/badge/Kibana-7.16.3-E8478B?style=flat&logo=kibana&logoColor=white)

## Overview

Deployment of a **Security Operations Center (SOC)** environment using the ELK Stack (Elasticsearch, Logstash, Kibana) on AWS EC2. The stack runs fully containerized via Docker and Docker Compose, with Logstash ingesting events into Elasticsearch and Kibana providing the visualization and analysis layer.

## Table of Contents

- [Architecture](#architecture)
- [Infrastructure](#infrastructure)
- [01 — EC2 Setup + Docker](./01-ec2-setup/)
- [02 — ELK Stack via Docker](./02-elk-docker/)
- [03 — ELK Stack via Docker Compose + Logstash](./03-elk-compose/)
- [04 — Kibana Index Pattern + Discover](./04-kibana-discover/)

---

## Architecture
```
Internet
    │
    ├── SSH     :22   (restricted to admin IP)
    ├── Kibana  :5601
    ├── Elastic :9200
    └── Logstash:5044
         │
         ▼
┌─────────────────────────────────┐
│  EC2 t3.large · Amazon Linux    │
│  Elastic IP (static)            │
│                                 │
│  ┌─────────────────────────┐    │
│  │  Docker                 │    │
│  │  sebp/elk:7.16.3        │    │
│  │                         │    │
│  │  Elasticsearch  :9200   │    │
│  │  Logstash       :5044   │    │
│  │  Kibana         :5601   │    │
│  └─────────────────────────┘    │
└─────────────────────────────────┘
```

## Infrastructure

| Component | Value |
|---|---|
| Cloud Provider | AWS |
| Instance Type | t3.large (2 vCPU · 8GB RAM) |
| OS | Amazon Linux |
| Storage | 30 GB |
| IP | Elastic IP (static) |
| ELK Image | sebp/elk:7.16.3 |
| Deployment | Docker · Docker Compose |

## What This Demonstrates

| Capability | Result |
|---|---|
| EC2 provisioning and hardening | ✅ |
| Security Group configuration | ✅ |
| Docker installation and management | ✅ |
| ELK Stack deployment via Docker | ✅ |
| ELK Stack deployment via Docker Compose | ✅ |
| Log ingestion via Logstash | ✅ |
| Data visualization in Kibana | ✅ |
| Index pattern creation and Discover | ✅ |
