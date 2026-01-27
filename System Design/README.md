### Project Architecture Diagram

![Project Architecture Diagram](logical%20architecture-update.drawio.png)

## Logical Flow of Project Architecture

The logical flow describes how the application moves through the DevSecOps pipeline
from source code to deployment and monitoring.

1. **Source Code Management**
   - Developer pushes code to GitHub repository.

2. **CI/CD Orchestration**
   - Jenkins pipeline is triggered automatically.
   - Jenkins controls the complete workflow.

3. **Code Quality & Build**
   - Jenkins sends source code to SonarQube for static code analysis.
   - If quality gate passes, the application is built.
   - Build artifacts and Docker images are stored in Nexus Repository.

4. **Security Scanning**
   - Trivy scans the file system and Docker images for vulnerabilities.
   - kube-audit checks Kubernetes cluster security configurations.

5. **Deployment**
   - Jenkins uses kubectl to deploy the application.
   - Application is deployed to the Kubernetes cluster (Master & Worker Nodes).

6. **Application Runtime**
   - Application runs inside Kubernetes Pods on worker nodes.

7. **Monitoring & Observability**
   - Prometheus collects metrics from Jenkins and application endpoints.
   - Blackbox Exporter monitors application uptime.
   - Grafana visualizes metrics using dashboards.



