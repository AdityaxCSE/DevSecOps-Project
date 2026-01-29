# n8n Setup – AI Automation & Workflow Orchestration

## Overview
**n8n** is used in this project as an **AI-enabled workflow automation and orchestration layer** that integrates with the CI/CD pipeline.  
It works alongside Jenkins to enable conditional logic, intelligent automation, notifications, and external integrations.

---

## Purpose
The purpose of using n8n is to:
- Extend CI/CD automation beyond standard pipeline logic
- Orchestrate workflows based on pipeline events
- Enable AI-driven or rule-based decision making
- Reduce manual intervention in DevSecOps processes

---

## Role in Project Architecture
In the logical architecture:
- Jenkins handles CI/CD execution
- n8n handles **workflow orchestration and automation**

n8n is triggered by Jenkins and can control downstream actions such as approvals, notifications, or conditional pipeline continuation.

---

## Deployment Location
- Deployed as a **standalone service**
- Runs close to CI/CD tooling (same server or network as Jenkins)
- Deployed using Docker for portability and simplicity

---

## Installation (Docker – Recommended)

```bash
docker run -d \
  --name n8n \
  -p 5678:5678 \
  n8nio/n8n
