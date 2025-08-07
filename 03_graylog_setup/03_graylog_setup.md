# 03 — Graylog Setup

---

## Scenario

This module focused on deploying Graylog in a Docker-based environment for log aggregation and analysis. The goal was to establish a working instance of Graylog, along with its required dependencies, MongoDB and Elasticsearch, while resolving resource and startup issues.

---

## What I Did

```bash
# Cloned and entered working directory
git clone https://github.com/[your-repo]/graylog-rebuild
cd graylog-rebuild

# Removed conflicting containers
sudo docker stop graylog mongo woe-mongo-1 woe-elasticsearch-1
sudo docker rm graylog mongo woe-mongo-1 woe-elasticsearch-1

# Edited docker-compose.yml
nano docker-compose.yml
```

Final `docker-compose.yml` used:

```yaml
version: '3.8'

services:
  mongo:
    image: mongo:5.0
    container_name: mongo
    networks:
      - graylog

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch-oss:7.10.2
    container_name: elasticsearch
    environment:
      - discovery.type=single-node
      - ES_JAVA_OPTS=-Xms1g -Xmx1g
    ulimits:
      memlock:
        soft: -1
        hard: -1
    mem_limit: 2g
    networks:
      - graylog

  graylog:
    image: graylog/graylog:5.1
    container_name: graylog
    environment:
      - GRAYLOG_PASSWORD_SECRET=somepasswordpepper
      - GRAYLOG_ROOT_PASSWORD_SHA2=766af3e91e94cb8e4e14fbdf040c9f37b0cc994f2fa6d44bf53617373641332a
      - GRAYLOG_HTTP_EXTERNAL_URI=http://localhost:9000/
      - GRAYLOG_ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    depends_on:
      - mongo
      - elasticsearch
    ports:
      - "9000:9000"
      - "12201:12201/udp"
    networks:
      - graylog

networks:
  graylog:
```

```bash
# Launched environment
sudo docker-compose up -d

# Verified container status
sudo docker ps

# Validated Elasticsearch response
sudo docker exec -it elasticsearch curl http://localhost:9200

# Checked Graylog startup logs
sudo docker logs graylog --tail 50

# Accessed Graylog at:
http://localhost:9000

# Credentials
Username: admin
Password: Graylog123!
```

---

## What I Learned

- Graylog requires at least 5GB of free space for the message journal.
- Elasticsearch and MongoDB must be online before Graylog starts.
- Graylog uses SHA256-hashed root passwords, generated manually.
- Proper memory and disk limits are critical in constrained lab environments.
- Logs and container health should always be verified before UI login attempts.

---

## Why It Matters

Deploying Graylog provides a centralized platform for analyzing and managing logs, which is critical in a blue team environment. Troubleshooting startup issues improves operational awareness of Docker-based deployments and their dependencies.

---
