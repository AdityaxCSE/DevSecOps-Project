# Security Step (DevSecOps)

## Purpose
The **Security Step** ensures that both the application and the infrastructure are protected against vulnerabilities and misconfigurations.  
This stage enforces **DevSecOps principles** by integrating security checks directly into the CI/CD pipeline.

---

## Tools Used
- **Trivy** – Vulnerability scanning for application file systems and Docker images
- **kube-audit** – Kubernetes cluster security auditing

---

## Security Scope
The security stage covers the following areas:
- Application source code and dependencies
- Docker images built during the pipeline
- Kubernetes cluster configurations and security settings

---

## Security Flow
1. The security step is triggered after the successful build stage.
2. Trivy scans application files and Docker images for known vulnerabilities.
3. Scan results are evaluated based on severity.
4. kube-audit audits Kubernetes cluster configurations against security best practices.
5. If critical security issues are detected, the pipeline is stopped.

---

## Outcome
- Early detection of security vulnerabilities and misconfigurations
- Prevention of insecure deployments
- Only **secure and compliant artifacts** are allowed to move to the deployment step

---

## Detailed Documentation
For detailed security tool usage, refer to:
- [Trivy Vulnerability Scanning](trivy-scan.md)
- [kube-audit Security Auditing](kube-audit.md)


