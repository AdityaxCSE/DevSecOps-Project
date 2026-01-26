# Trivy Vulnerability Scanning

## Purpose
Trivy is used to scan file systems and Docker images
for known vulnerabilities.

## Installation Location
- Installed on Jenkins server

## Scan Types
- File system scan
- Docker image scan

## Pipeline Integration
- Jenkins runs Trivy scan after build
- If critical vulnerabilities are found, the pipeline fails
