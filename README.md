# 🔐 Secure CI/CD Pipeline with Kubernetes (DevSecOps)

## 📌 Overview
This project implements a **production-grade DevSecOps CI/CD pipeline** that automates application delivery with integrated security, AI-driven analysis, and full observability.

It demonstrates how modern organizations build **secure, scalable, and automated deployment systems** using industry tools like Jenkins, Kubernetes, SonarQube, Trivy, Nexus, Prometheus, Grafana, and n8n.

---

## 🎯 Objectives
- Automate the complete software delivery lifecycle  
- Integrate **security at every stage (Shift Left Security)**  
- Deploy applications on a **scalable Kubernetes cluster**  
- Enable **AI-driven vulnerability analysis**  
- Provide **real-time monitoring and alerting**  

---

## 🏗️ Architecture Overview

The system follows a **layered architecture**, ensuring separation of concerns and scalability.

### 🔹 Core Layers:
1. **CI/CD Automation Layer** – Jenkins pipeline execution  
2. **Security Layer** – Code and container vulnerability scanning  
3. **Artifact Management Layer** – Nexus repository  
4. **Container Orchestration Layer** – Kubernetes cluster  
5. **AI Automation Layer** – n8n workflow with Gemini API  
6. **Monitoring Layer** – Prometheus + Grafana  

---

## 📊 Architecture Diagram
![Architecture](System%20Design/logical%20architecture-final.drawio.png)

---

## 🤖 n8n Automation Workflow
![n8n Pipeline](https://drive.google.com/uc?export=view&id=1k7e-hpPvSj-64ZkdebVMInltUOkiSXCh)

---

## ⚙️ CI/CD Pipeline Stages

### 🧱 1. Build Stage (CI)
- Triggered via GitHub webhook  
- Code is compiled and tested using Maven  
- Code quality analysis using SonarQube  

---

### 🔐 2. Security Stage (DevSecOps)
- **Trivy File System Scan** – detects vulnerabilities in dependencies  
- **Trivy Image Scan** – scans Docker images before deployment  
- Ensures only secure artifacts move forward  

---

### 📦 3. Artifact Management
- Docker images are pushed to **Nexus Repository**  
- Provides centralized and version-controlled artifact storage  

---

### 🚀 4. Deployment Stage (CD)
- Application deployed to **Kubernetes cluster**  
- Uses `kubectl` for automated deployment  
- Deployment verification ensures successful rollout  

---

### 📊 5. Monitoring & Observability
- **Prometheus** collects system and cluster metrics  
- **Grafana** visualizes dashboards  
- Enables real-time monitoring and alerting  

---

### 🤖 6. AI-Driven Security Analysis
- Trivy scan reports generate CVE data  
- n8n workflow triggers automatically  
- Gemini API analyzes vulnerabilities  
- Generates human-readable reports  
- Sends notification after pipeline completion  

---

## 🔄 End-to-End Workflow

```text
Developer Push → Jenkins Trigger → Build & Test → Security Scan →
Docker Build → Image Scan → Push to Nexus →
Deploy to Kubernetes → Monitoring →
CVE Extraction → AI Analysis (n8n + Gemini) → Notification
