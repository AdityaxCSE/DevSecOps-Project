# Artifact Management Stage (Nexus Repository)

## Purpose
The **Artifact Management Stage** is responsible for storing, versioning, and managing build outputs generated during the CI/CD pipeline.  
This stage ensures that only validated and versioned artifacts are preserved for deployment and future use.

---

## Role of Nexus in the Build Stage
Nexus Repository is used as a **centralized artifact repository** to store build artifacts and container images produced by Jenkins.

---

## Artifact Management Responsibilities
- Store build artifacts (JAR, WAR, binaries, Docker images)
- Maintain versioned artifacts for traceability
- Provide a single source of truth for deployment artifacts
- Integrate securely with Jenkins pipelines
- Support rollback and reproducible builds

---

## Build Flow Integration
1. Jenkins completes the build process successfully.
2. Jenkins packages the application or builds Docker images.
3. Jenkins authenticates with the Nexus Repository.
4. Build artifacts and container images are pushed to Nexus.
5. Nexus stores and manages artifacts by version.

---

## Output of This Stage
- Versioned build artifacts stored in Nexus
- Container images ready for deployment
- Reliable artifact source for downstream pipeline stages

---

## Reference
For Nexus installation and repository configuration, refer to:  
[Nexus Setup](../docs/nexus-setup.md)
