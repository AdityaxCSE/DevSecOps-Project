# SonarQube Setup

## Purpose
SonarQube is used for static code analysis to identify bugs, vulnerabilities,
and code smells.

## Deployment Method
- SonarQube is deployed as a Docker container
- Image: sonarqube:lts-community
- Port: 9000

## Integration
- Jenkins sends source code to SonarQube
- Quality Gate must pass to continue pipeline
