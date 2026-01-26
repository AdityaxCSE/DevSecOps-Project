# Build Step (CI/CD & Code Quality)

## Purpose
The build step is responsible for compiling source code, performing static code analysis,
and storing build artifacts.

## Tools Used
- Jenkins (CI/CD Orchestration)
- SonarQube (Code Quality Analysis)
- Nexus Repository (Artifact Storage)

## Build Flow
1. Developer pushes code to GitHub.
2. Jenkins pipeline is triggered automatically.
3. SonarQube performs static code analysis.
4. Build artifacts and Docker images are stored in Nexus.
5. If all checks pass, the pipeline proceeds to the next stage.
