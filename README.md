
## Overview

This project demonstrates a **secure CI pipeline** for Dockerized applications using **DevSecOps principles**. The pipeline integrates **security scanning, secret detection, and compliance checks** directly into the CI workflow to prevent vulnerabilities from reaching production-level code.

The **main objective** was to gain hands-on experience in **building a DevSecOps pipeline**, applying **shift-left security practices**, and automating **image and code security checks**.

The pipeline was tested using the **OWASP Juice Shop**, a deliberately vulnerable web application, making it an excellent environment for experimenting **real-world vulnerability scanning and secret detection** in a safe context.

By completing this project, I learned how to:

- Embed **security into CI pipelines** to reduce risks early.
    
- Detect **hardcoded secrets, misconfigurations, and vulnerable packages**.
    
- Generate a **Software Bill of Materials (SBOM)** for compliance and supply chain visibility.

## 🛠️ Technologies Used

- **[Trivy](https://trivy.dev/latest/)** – Vulnerability and misconfiguration scanner
    
- **[Dockle](https://github.com/goodwithtech/dockle)** – Docker image configuration linting
    
- **[Trufflehog](https://github.com/trufflesecurity/trufflehog)** – Secret scanning across the repository
    
- **OWASP ZAP** – Passive web application vulnerability scanner
    
- **Docker & Docker Compose** – Containerization and orchestration
    
- **GitHub Actions** – CI automation

## Workflow 

The **Secure-CI** pipeline runs automatically on **pull requests** to the `main` and `staging` branches. It performs **five security-focused jobs:

1. **Docker Image Vulnerability Scan (Trivy)**
    
    - Scans the `bkimminich/juice-shop` image for known vulnerabilities.
        
2. **Secret Scanning (Trufflehog)**
    
    - Detects any exposed credentials, tokens, or API keys in the repository’s commit history regardless of branches.
        
3. **Docker Image Configuration Check (Dockle)**
    
    - Flags misconfigurations and best-practice issues in the Docker image.
        
4. **SBOM Generation (Trivy)**
    
    - Creates a **Software Bill of Materials** for supply chain visibility and uploads it as a pipeline artifact. It also includes vulnerabilities found for later analysis. 
        
5. **Passive Web Application Scan (OWASP ZAP)**
    
    - Builds and runs the Dockerized app, then performs a **passive vulnerability scan** on HTTP traffic without actively interacting with the app.


Feel free to **use this workflow** to secure your own Dockerized projects. 🙂

For a **detailed explanation of the implementation, tools, and DevSecOps principles**, check out the Medium article I wrote on it:  https://medium.com/@martin.yordanov.official/devsecops-building-a-secure-ci-pipeline-7915f040ca94
