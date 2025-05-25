# Monitoring and Logging in DevOps

## PromQL

It helps you rerive and analyse the timeseries data stored in prometheus database.
- Filtering with labels {}
- Range queries []
- Functions
- Aggregation Functions
- Binary Operators
## Prometheus Monitoring Metrics

### OS Level Metrics
- CPU
- Memory
- Disk
- Network, etc.

To get all these, An Agent needs to be installed on a Linux server to expose Hardware and OS leve metrics, which is called **Node Exporter**.
Prometheus itself does not collect system level metrics.Instead it relies on exporters to provide data, which is **Node Exporter**.

How does a Node Exporter works,
- It is runs as daemon on the machine
- It exposes metrics on http://host-ip:9091/metrics
- The prometheus connect to the metrics endpoing  and pull data at regular intervals.

## Setting up and Monitoring with Node Exporter 
- Download and set up the Node Exporter on localhost
```bash
$ sudo wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-arm64.tar.gz
$ sudo tar xvfz node_exporter-*.*-arm64.tar.gz
$ sudo rm node_exporter-1.8.2.linux-arm64.tar.gz
$ sudo mkdir node_exporter
$ sudo mv node_exporter-*.linux-arm64/* ./node_exporter
$ cd node_exporter
$ sudo ./node_exporter > /dev/null 2>&1 &
$ curl http://localhost:9100/metrics
```
- Set up a Prometheus server on localhost to scrape Node 
```bash
$ cd prometheus
$ sudo vim prom-node-exporter.yaml
```
and copy, paste and save the following content
```YAML
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: node_exporter
    static_configs:
      - targets:
          - localhost:9100
```
```bash
$ sudo prometheus --config.file=prom-node-exporter.yaml
```
- Access Node Exporter metrics using Prometheus UI(http://localhost:9090)

