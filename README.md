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

## Configure InflixDB database
### Create Telegraf and Prometheus database
```
curl -XPOST -G "http://localhost:9086/query?pretty=true" --data-urlencode "q=CREATE DATABASE telegraf"
curl -XPOST -G "http://localhost:9086/query?pretty=true" --data-urlencode "q=CREATE DATABASE prometheus"
```

### Add retention policy (Optional)

```
curl -XPOST -G "http://localhost:9086/query?pretty=true" --data-urlencode 'q=CREATE RETENTION POLICY "default" ON "telegraf" DURATION 30d REPLICATION 1 DEFAULT'
```