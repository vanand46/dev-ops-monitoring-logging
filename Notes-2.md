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

## Writing Basic Queries in PromQL
- Navigate to the browser and enter the URL http://localhost:9090/ or http://<public-ip>:9090/ to access the Prometheus console
- Navigate to the Graph section
- Enter the following query in the expression browser to retrieve a single metric, then click on Execute:**node_cpu_seconds_total**
- Filter by label : **node_filesystem_avail_bytes{device='/dev/root'}**
    - **node_filesystem_avail_bytes**: This metric represents the number of available bytes on the filesystem. It's commonly used to monitor disk space.
    - **{device="/dev/"}**: This filter selects only those metrics where the device label is exactly equal to "/dev/".
- Aggregate data with the sum() function: **sum(node_network_transmit_bytes_total)**
    - **node_network_transmit_bytes_total**: This metric represents the total number of bytes transmitted over all network interfaces since the system started.
    - **sum(...)**: Aggregates the total transmitted bytes across all instances and network interfaces
- Query data using an arithmetic operation:**node_memory_MemAvailable_bytes/1024/1024**
    - **node_memory_MemAvailable_bytes**: This metric gives the amount of memory available for new allocations in bytes.
    - **/1024/1024**: Divides the value by 1024 twice to convert bytes into megabytes (MB).
- Calculate a metric using the rate() function: **rate(node_network_receive_bytes_total[1m])** 
    - **node_network_receive_bytes_total**: This metric represents the total number of bytes received on all network interfaces since the system started (a cumulative counter).
    - **rate(...)**: Calculates the per-second rate of change (bytes per second) for the specified metric over the given time range.
    - **[1m]**: Specifies a time window of 1 minute to calculate the rate of incoming traffic.

