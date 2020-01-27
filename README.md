# What is in this repository?

This repository contains easily deployable monitoring solution which uses:
 - Grafana (frontend for monitoring + alerts)
 - Prometheus (monitoring solution pulling metrics from exporter)
 - Node Exporter for Prometheus (metrics exporter-exposer for Prometheus)
 - Telegraf (monitoring agent)
 - InfluxDB (persistent timeseries storage)

# How to use it?

If you have docker and docker-compose installed, this will take roughly 1 minute to have it up and running.
If not - it will still take mentioned ~ 1 minute + time needed for docker installation.

# Requirements

|Container           |MEM         |CPU     |Storage        |
|--------------------|------------|--------|---------------|
|Grafana             |255 MB      |1       |at least 100 MB|
|Influxdb            |4   GB      |1       |at least 10  GB|
|node-exporter       |50  MB      |1       |-              |
|telegraf            |50  MB      |1       |-              |
|prometheus          |150 MB      |1       |-              |

## Configure InflixDB database
### Create Telegraf and Prometheus database
```
curl -X POST -G "http://localhost:9086/query?pretty=true" --data-urlencode "q=CREATE DATABASE telegraf"
curl -X POST -G "http://localhost:9086/query?pretty=true" --data-urlencode "q=CREATE DATABASE prometheus"
```

### Add retention policy (Optional)

```
curl -XPOST -G "http://localhost:9086/query?pretty=true" --data-urlencode 'q=CREATE RETENTION POLICY "default" ON "telegraf" DURATION 30d REPLICATION 1 DEFAULT'
```