# Monitoring Stack

This document explains the monitoring and observability setup.

## Monitoring Components
- **Prometheus**
  - Collects system and cluster metrics
  - Runs on port 9090
- **Grafana**
  - Visualizes metrics and dashboards
  - Runs on port 3000
- **Node Exporter**
  - Collects Jenkins server system metrics
- **Blackbox Exporter**
  - Monitors application uptime and HTTP endpoints

## Configuration
- Update `prometheus.yml` to add:
  - Jenkins Node Exporter
  - Kubernetes targets
  - Application endpoints

## Outcome
Centralized monitoring with real-time dashboards and alerts.

