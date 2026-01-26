### Project Architecture Diagram

![Project Architecture Diagram](project-architecture.png)

This project follows a layered DevSecOps system design.

- The Kubernetes Cluster consists of one Master node and two Worker nodes.
- Jenkins acts as the CI/CD orchestrator and manages the pipeline.
- SonarQube performs static code analysis during the build stage.
- Nexus stores build artifacts and Docker images.
- Jenkins deploys applications to the Kubernetes cluster using kubectl.
- Prometheus collects metrics from Jenkins and application endpoints.
- Grafana visualizes system and application metrics using dashboards.

