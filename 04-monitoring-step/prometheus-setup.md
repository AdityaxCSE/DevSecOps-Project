# Prometheus Setup

## Purpose
Prometheus is used to **collect and store metrics** from Jenkins, Kubernetes components, and application endpoints.  
It provides the core metrics backend for monitoring and observability in this project.

---

## Service Details
- **Port:** 9090
- **Role:** Metrics collection and time-series storage

---

## Metrics Collection Scope
Prometheus collects metrics from the following targets:
- **Jenkins Server**
  - System metrics exposed via Node Exporter
- **Application Services**
  - Application and service-level metrics
- **Kubernetes Components**
  - Cluster and workload metrics (if enabled)

---

## Configuration
- Monitoring targets are defined in the `prometheus.yml` configuration file.
- The configuration includes scrape jobs for:
  - Jenkins Node Exporter
  - Application service endpoints
- Each target is defined using its IP address or service endpoint and port.

---

## Monitoring Flow
1. Prometheus periodically scrapes metrics from configured targets.
2. Collected metrics are stored as time-series data.
3. Metrics are made available for visualization and alerting through Grafana.

---

## Outcome
- Centralized metrics collection
- Real-time visibility into system and application performance
- Reliable data source for dashboards and alerts

---

## Reference
For full monitoring stack details, refer to:  
[Monitoring Stack Overview](../docs/monitoring-stack.md)
