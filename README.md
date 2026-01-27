#  End-to-End DevSecOps Kubernetes Project

##  Project Overview
This project demonstrates a complete **DevSecOps pipeline** deployed on a **Kubernetes cluster** with integrated **CI/CD, security scanning, artifact management, and monitoring**.

##  Infrastructure Architecture
- Kubernetes Cluster (1 Master, 2 Worker Nodes)
- Jenkins CI/CD Server
- SonarQube for Code Quality
- Nexus Repository Manager
- Trivy for Security 
- Prometheus & Grafana for Monitoring

## Security Tools Used
- Trivy (Image & File System Scanning)
- kube-audit (Kubernetes Security Auditing)

## Monitoring Stack
- Prometheus
- Grafana
- Blackbox Exporter

##  Tools & Technologies
| Tool | Purpose |
|----|----|
| Kubernetes | Container Orchestration |
| Jenkins | CI/CD Automation |
| SonarQube | Static Code Analysis |
| Nexus | Artifact Repository |
| Trivy | Vulnerability Scanner |
| Prometheus | Metrics Collection |
| Grafana | Visualization |

## Documentation Index

- [Kubernetes Setup](docs/kubernetes-setup.md)
- [Jenkins Setup](docs/jenkins-setup.md)
- [SonarQube Setup](docs/sonarqube-setup.md)
- [Nexus Setup](docs/nexus-setup.md)
- [Security Tools](docs/security-tools.md)
- [Monitoring Stack](docs/monitoring-stack.md)


