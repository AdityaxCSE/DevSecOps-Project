## Jenkins CI/CD Pipeline Stages

This pipeline automates build, security scanning, artifact management, containerization, Kubernetes deployment, and AI-driven vulnerability analysis.

---

### 1. Build (Trigger Stage)
Initial stage confirming that the pipeline execution was triggered successfully via GitHub webhook.

**Purpose:**  
- Acts as pipeline entry confirmation  
- Improves traceability of webhook-based executions  

---

### 2. Git Checkout
Fetches the latest source code from the main branch of the GitHub repository.

**Purpose:**  
- Ensures pipeline runs on the most recent commit  
- Provides source code for build and security scans  

---

### 3. Compile
Compiles the application source code using Maven.

**Purpose:**  
- Validates code syntax and structure  
- Detects compilation errors early  

---

### 4. Test
Executes unit tests using Maven.

**Purpose:**  
- Verifies application logic correctness  
- Prevents faulty code from progressing in the pipeline  

---

### 5. File System Scan (Trivy – SCA)
Performs a file system–level vulnerability scan on the project workspace.

**Purpose:**  
- Detects known vulnerabilities in third-party dependencies  
- Implements shift-left security using Software Composition Analysis (SCA)  

**Output:**  
- `trivy-fs-report.html`

---

### 6. SonarQube SAST Scan
Runs Static Application Security Testing (SAST) using SonarQube.

**Purpose:**  
- Identifies code smells, bugs, and security vulnerabilities  
- Enforces secure coding standards  

---

### 7. Quality Gate
Evaluates the SonarQube Quality Gate status.

**Purpose:**  
- Ensures minimum code quality and security thresholds  
- Prevents poor-quality code from moving forward  

---

### 8. Build Application
Packages the application into a deployable artifact using Maven.

**Purpose:**  
- Produces final application binaries  
- Required for artifact publishing and containerization  

---

### 9. Publish Artifacts to Nexus
Uploads the built artifacts to Nexus Repository Manager.

**Purpose:**  
- Centralized artifact storage  
- Enables dependency management and version control  

---

### 10. Build Docker Image
Builds a Docker image using the packaged application.

**Purpose:**  
- Creates a portable and consistent runtime environment  
- Tags image using Jenkins build number for traceability  

---

### 11. Docker Image Scanning (Trivy)
Scans the Docker image for OS-level and application-level vulnerabilities.

**Purpose:**  
- Detects CRITICAL and HIGH CVEs in container images  
- Prevents insecure images from deployment  

**Output:**  
- `trivy-image-report.html`

---

### 12. Push Docker Image
Pushes the scanned Docker image to Docker Hub.

**Purpose:**  
- Makes image available for Kubernetes deployment  
- Ensures only scanned images are published  

---

### 13. Deploy to Kubernetes
Deploys the Docker image to the Kubernetes cluster.

**Purpose:**  
- Automates application deployment  
- Updates image version dynamically using build tag  

---

### 14. Verify Deployment
Validates the Kubernetes deployment and services.

**Purpose:**  
- Confirms pods and services are running correctly  
- Ensures successful application rollout  

---

### 15. Extract CRITICAL CVEs
Extracts unique CRITICAL CVE IDs from Trivy scan reports.

**Purpose:**  
- Filters high-risk vulnerabilities  
- Prepares data for automated security analysis  

**Output:**  
- `critical-cves.txt`

---

### 16. Send CVEs to n8n for AI Analysis
Sends extracted CRITICAL CVEs to n8n via webhook.

**Purpose:**  
- Triggers AI-based vulnerability analysis  
- Automates risk assessment and remediation insights  

---

## Post Actions

### Artifact Archiving
Archives security reports and CVE data.

**Archived Files:**  
- `trivy-fs-report.html`  
- `trivy-image-report.html`  
- `critical-cves.txt`  

---

### Email Notification
Sends pipeline execution status and security reports via email.

**Purpose:**  
- Notifies stakeholders of pipeline result  
- Provides audit trail and security visibility  

---

## Pipeline Summary
- End-to-end DevSecOps automation  
- Shift-left security (SAST + SCA)  
- Container and Kubernetes security  
- AI-assisted vulnerability intelligence  
- Production-style CI/CD workflow  
