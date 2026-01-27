# SonarQube Setup

This document covers the setup of **SonarQube** for static code quality analysis.

## Installation Method
- Install Docker engine
- Run SonarQube as a Docker container:
  ```bash
  docker run -d \
    -p 9000:9000 \
    --name sonarqube \
    sonarqube:lts-community
  
## Configuration

- Access SonarQube via port 9000
- Configure quality gates
- Integrate SonarQube with Jenkins pipeline

## Outcome

Automated static code analysis enforcing quality standards.
