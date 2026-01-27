# Build Pipeline Overview

## Purpose
This document explains how the **build stage** of the CI/CD pipeline works and how Jenkins orchestrates build activities.

## Role of Jenkins in Build Stage
Jenkins acts as the CI/CD automation server responsible for executing the build workflow.

## Build Responsibilities
- Automatically trigger the pipeline when code is pushed to GitHub
- Pull the latest source code from the repository
- Integrate with SonarQube for static code quality analysis
- Build application artifacts or Docker images
- Push build artifacts and images to the Nexus Repository

## Build Outcome
- Quality-validated source code
- Versioned build artifacts stored in Nexus
- Successful handoff to the next pipeline stage

## Reference
For Jenkins installation and configuration details, see:  
[Jenkins Setup](../docs/jenkins-setup.md)
