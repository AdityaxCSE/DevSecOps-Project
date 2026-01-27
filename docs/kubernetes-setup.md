# Kubernetes Setup

This document describes the setup of a **3-node Kubernetes cluster** consisting of one Master node and two Worker nodes.

## Master Node Configuration
- Install container runtime (Docker dependencies)
- Install Kubernetes components:
  - kubeadm
  - kubelet
  - kubectl
- Initialize the cluster:
  ```bash
  kubeadm init

Configure kubectl access for the admin user

Install kube-audit to scan cluster configurations for security issues

## Worker Node Configuration

Install container runtime

Install kubeadm, kubelet, and kubectl

Join the cluster using the command generated on the Master node:

kubeadm join <master-ip>:6443 --token <token>

## Outcome
A functional Kubernetes cluster capable of running containerized workloads.
