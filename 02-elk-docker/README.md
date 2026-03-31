# 02 — ELK Stack Deployment via Docker

## Overview

Deploy the full ELK stack (Elasticsearch, Logstash, Kibana) as a single container using the `sebp/elk` image. Verify Kibana is accessible and all three services are running correctly.

---

## Step 1 — Configure vm.max_map_count

Elasticsearch requires a higher virtual memory limit than the Linux default. Without this, Elasticsearch fails to start silently.
```bash
sudo sysctl -w vm.max_map_count=262144
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf
```

The second command makes the setting persistent across reboots.

---

## Step 2 — Pull and Run ELK Container
```bash
docker pull sebp/elk:7.16.3

docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 \
  -it --name elk -d --hostname elk sebp/elk:7.16.3
```

![ELK Running](../screenshots/17.png)

| Port | Service |
|---|---|
| 5601 | Kibana |
| 9200 | Elasticsearch |
| 5044 | Logstash |

The container starts all three ELK services internally. Initial startup takes 2-3 minutes while Elasticsearch and Kibana initialize.

---

## Step 3 — Kibana Verification

![Kibana UI](../screenshots/18.png)

Kibana accessible at `http://<ELASTIC_IP>:5601` confirming the full ELK stack is running correctly.
