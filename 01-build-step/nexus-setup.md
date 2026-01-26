# Nexus Repository Setup

## Purpose
Nexus is used to store build artifacts and Docker images securely.

## Deployment Method
- Nexus runs as a Docker container
- Image: sonatype/nexus3
- Port: 8081

## Usage
- Jenkins pushes build artifacts to Nexus
- Artifacts are reused during deployment
