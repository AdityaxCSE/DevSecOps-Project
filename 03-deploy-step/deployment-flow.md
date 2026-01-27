# Kubernetes Deployment Flow

## Purpose
This document describes the **deployment flow** used to deploy applications into a Kubernetes cluster as part of the CI/CD pipeline.

---

## Deployment Flow
1. Jenkins triggers the deployment stage after successful build and security checks.
2. Jenkins uses `kubectl` to apply Kubernetes manifests (Deployment, Service, ConfigMap, etc.).
3. The Kubernetes API Server receives and validates the deployment request.
4. The Kubernetes Scheduler assigns application Pods to suitable worker nodes.
5. kubelet on each worker node starts the assigned Pods.
6. Kubernetes Services expose the application according to the configured service type.

---

## Deployment Outcome
- Application Pods are running successfully on worker nodes
- Services provide stable access to the application
- Deployment is automated, repeatable, and controlled

---

## Reference
For Kubernetes cluster setup and configuration details, refer to:  
[Kubernetes Setup](../docs/kubernetes-setup.md)
