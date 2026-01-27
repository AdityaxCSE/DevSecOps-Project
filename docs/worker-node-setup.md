# Worker Node Setup

## Responsibilities
Worker nodes are responsible for:
- Running application Pods scheduled by the Kubernetes Master
- Executing containerized workloads
- Communicating with the Master node for scheduling and status updates

---

## Key Setup Steps

### 1. Install Container Runtime
Install the required container runtime dependencies to allow Kubernetes to run containers.

---

### 2. Install Kubernetes Components
Install the following Kubernetes tools on each worker node:
- **kubeadm** – Used to join the node to the cluster
- **kubelet** – Node-level agent that manages Pods and containers

> Note: `kubectl` is optional on worker nodes and is mainly required on the master or CI/CD server.

---

### 3. Join the Cluster
Join the worker node to the Kubernetes cluster using the command generated on the master node:

```bash
kubeadm join <master-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>

