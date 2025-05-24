# Monitoring and Logging in DevOps

They are the part of the monitor phase of the DevOps lifecycle.
The infrastructure setup to perform monitoring and logging activities is called monitoring and logging system.

They aim to Identify
- Resource Utilization
- Container Monitoring
- Possible Disaster

## Introduction to Monitoring and Prometheus

### Monitoring
Used for tracking the,
- Performance
- Availability
- Security

of the applications, systems and infrastructure real time.

### Logging
For recording and storing detailed information about,
- System Events
- Errors
- User Activities 

within applications or infrastructure.

## Continuous Monitoring
Skill that helps in tracking real time system performace using monitoring system.
It includes,
- Data collection
- Data analysis
- Data action

The most used tools are,
- Prometheus
- Grafana
- ELK
- Datadog
- New Relic
- Splunk
- AppDynamics

**Prometheus** - Used for monitoring systems and services, especially in cloud-native environments with Kubernetes.

**Grafana** - Used for visualizing metrics and logs with customizable dashboard across multiple data sources

**ELK** Used for log aggregation, search, and visualization in large-scale data analytics.

## Types of Monitoring
Categorized based on different aspects or components
- **Application Performance Monitoring**: How well the code is performing
    - Datadog
    - New Relic
- **Infrastructure Monitoring**: Tracks Servers, Containers, VMs, Cloud resources.
    - Prometheus
- **Network Monitoring**: Monitors the network traffic, latency, packetloss, availability.
- **Log Monitoring**: Analyse the logs from application, servers and systems
- **Synthetic Monitoring**: Simulates the user behaviours by sending fake traffic.
- **Real User Monitoring**: Real time monitoring and alerting.

## Prometheus
Widely used tool for monitoring and alerting.It is used for application built with containers, microservices or cloud technology.

Key Features are:

- Data Model
- Query Language(PromQL)
- Independent Operation 
- Data Collection Method
- Target Discovery
- Visualization

To start prometheus service(in ubuntu)
```bash
$ sudo service prometheus start
```
Please go to browser and check http://localhost:9090

Go to prometheus folder and please see the content of the prometheus.yml which is the configuration file of the prometheus.
```bash
$ cat prometheus.yml
```

## Running Prometheus as a Docker Container for Monitoring
1. **Pull and set up Docker environment**
```bash
$ sudo docker pull prom/prometheus
```
2. Execute the following command on the terminal to create a Docker network
```bash
$ sudo docker network create prometheus-net 
```
3. Run the following commands to create a new directory named prometheus-docker, store the Prometheus configuration file in it.
```bash
$ mkdir prometheus-docker
$ cd prometheus-docker/
$ sudo vim prometheus.yml
```
Copy and paste the following content and save the file.
```YAML
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']  
```
4. Start the Prometheus container
```bash
$ sudo docker run -d -p 9090:9090 --name prometheus --network prometheus-net -v prometheus.yml prom/prometheus
$ sudo docker ps
```

5. 4: Access the Prometheus web interface
Open the browser and enter the URL http://localhost:9090