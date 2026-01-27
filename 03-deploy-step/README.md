# Deployment Step (Kubernetes)

## Purpose
The **Deployment Step** is responsible for deploying validated and secure application artifacts into a Kubernetes cluster in an automated and controlled manner.

---

## Kubernetes Cluster Overview
The application is deployed to a Kubernetes cluster consisting of:
**1 Master Node (Control Plane)**
**2 Worker Nodes**

The cluster manages pod scheduling, scaling, and service availability.

---

## Deployment Tool
- **kubectl** – Used by Jenkins to apply Kubernetes manifests and manage application deployments

> Note: Cluster initialization tools such as `kubeadm` and runtime components like `kubelet` are part of the infrastructure setup and are not directly involved in the deployment stage.

---

## Deployment Flow
1. The deployment step is triggered after successful build and security stages.
2. Jenkins uses `kubectl` to apply Kubernetes manifests (Deployment, Service, etc.).
3. The Kubernetes Master schedules application pods on available Worker Nodes.
4. Kubernetes continuously monitors pod health and restarts failed pods if required.

---

## Outcome
- Application pods are successfully deployed and running in the Kubernetes cluster
- Services are exposed according to deployment configuration
- Automated and repeatable deployments are achieved

---

## Reference
For Kubernetes cluster setup and configuration, refer to:  
[Kubernetes Setup](../docs/kubernetes-setup.md)
