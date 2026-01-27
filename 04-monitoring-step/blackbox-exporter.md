# Blackbox Exporter

## Purpose
Blackbox Exporter is used to monitor **application availability and uptime** by probing endpoints using HTTP requests.  
It helps detect service outages and accessibility issues from an external perspective.

---

## Service Details
- **Port:** 9115
- **Role:** Endpoint probing and availability monitoring

---

## Monitoring Scope
Blackbox Exporter is used to monitor:
- Application HTTP endpoints
- Service availability and response status
- Basic latency and response success/failure

---

## Usage in Monitoring Flow
1. Blackbox Exporter exposes probe metrics on port 9115.
2. Prometheus is configured to scrape Blackbox Exporter endpoints.
3. Prometheus sends probe requests to target application URLs.
4. Probe results are collected as metrics.
5. Grafana visualizes availability status and uptime trends.

---

## Outcome
- Continuous monitoring of application availability
- Early detection of downtime or unreachable services
- Improved reliability and user experience

---

## Reference
For full monitoring configuration, refer to:  
[Monitoring Stack Overview](../docs/monitoring-stack.md)
