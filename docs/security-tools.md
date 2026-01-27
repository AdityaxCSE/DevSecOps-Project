# Security Tools

This document outlines the security tools integrated into the pipeline.

## Tools Used
- **Trivy**
  - File system scanning
  - Container image vulnerability scanning
- **kube-audit**
  - Kubernetes cluster security auditing

## Integration Points
- Trivy runs during Jenkins pipeline execution
- kube-audit scans the Kubernetes control plane configuration

## Outcome
Early detection of vulnerabilities following DevSecOps principles.
