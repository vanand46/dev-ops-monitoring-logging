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