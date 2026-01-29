# Secure CI/CD Pipeline with Kubernetes (DevSecOps)

## Project Overview
This project implements an end-to-end DevSecOps CI/CD pipeline using Jenkins, Kubernetes, AI-driven automation (n8n), and modern monitoring tools.
It automates source code validation, security scanning, artifact storage, deployment, and observability, following real-world industry best practices.

---

## Architecture Overview
The system follows a layered logical architecture that separates CI/CD automation, AI-driven workflow orchestration, application runtime, and monitoring.

### Project Architecture Diagram
![Project Architecture Diagram](System%20Design/logical%20architecture-final.drawio.png)


---

## Documentation Index
Detailed setup and configuration guides for each major component:

- [Kubernetes Setup](docs/kubernetes-setup.md)
- [Jenkins Setup](docs/jenkins-setup.md)
- [SonarQube Setup](docs/sonarqube-setup.md)
- [Nexus Setup](docs/nexus-setup.md)
- [Security Tools](docs/security-tools.md)
- [Monitoring Stack](docs/monitoring-stack.md)
- [AI Automation (n8n)](docs/n8n-setup.md)
---

## CI/CD Pipeline Stages
The CI/CD pipeline is organized into clear, modular stages:

- [01 – Build Step (CI/CD & Code Quality)](01-build-step/README.md)
- [02 – Security Step](02-security-step/README.md)
- [03 – Deploy Step (Kubernetes)](03-deploy-step/README.md)
- [04 – Monitoring Step](04-monitoring-step/README.md)

---

## End-to-End Workflow Summary
1. A developer pushes code to the source repository.
2. Jenkins triggers the CI/CD pipeline automatically.
3. Static code quality analysis and security scans are performed.
4. Build artifacts and container images are stored in Nexus.
5. Applications are deployed to the Kubernetes cluster.
6. Prometheus collects system and cluster metrics.
7. Grafana visualizes dashboards and alerts.

---

## Key Features
- Automated CI/CD pipeline
- Integrated security (DevSecOps)
- Kubernetes-based deployment
- Centralized artifact management
- Full monitoring and observability
- Industry-aligned project structure

---

## Intended Audience
- DevOps learners and students
- Academic project evaluation
- CI/CD and Kubernetes interview preparation
- DevSecOps practice environments

---

## License
This project is for educational and demonstration purposes.



