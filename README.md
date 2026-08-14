# DevSecOps Secure CI Pipeline
This project demonstrates a **secure CI pipeline** for Dockerized applications using **DevSecOps principles**. The pipeline integrates **security scanning, secret detection, and compliance checks** directly into the CI workflow to prevent vulnerabilities from reaching production-level code.

The pipeline was tested against the **OWASP Juice Shop**, a deliberately vulnerable web application, making it an excellent environment for experimenting **real-world vulnerability scanning and secret detection** in a safe context.

For a deep dive into the project, <a href='https://medium.com/@martin.yordanov.official/devsecops-building-a-secure-ci-pipeline-7915f040ca94'>check out my Medium article.</a>
## Table of Contents

1. [The motivation behind the project](#the-motivation-behind-the-project)
2. [What I strived to achieve and learn through this project](#what-i-strived-to-achieve-and-learn-through-this-project)
3. [Tech Stack](#tech-stack)
4. [Workflow](#workflow)
5. [Pipeline Testing](#Pipeline-Testing)
6. [Results](#Results)

## The motivation behind the 

## What I strived to achieve and learn through this project
The **main objective** was to gain hands-on experience in **building a DevSecOps pipeline**, applying **shift-left security practices**, and automating **image and code security checks**.

Through this project I learned how to:
- Embed **security into CI pipelines** to reduce risks early.
    
- Detect **hardcoded secrets, misconfigurations, and vulnerable packages** within the entire repository.
    
- Generate a **Software Bill of Materials (SBOM)** for compliance purposes as well as supply chain visibility.

## Tech Stack
The pipeline makes use of the following tools:
- **[Trivy](https://trivy.dev/latest/)** – Vulnerability and misconfiguration scanner
    
- **[Dockle](https://github.com/goodwithtech/dockle)** – Docker image configuration linting
    
- **[Trufflehog](https://github.com/trufflesecurity/trufflehog)** – Secret scanning across the repository
    
- **OWASP ZAP** – Passive web application vulnerability scanner
    
- **Docker & Docker Compose** – Containerization and orchestration
    
- **GitHub Actions** – CI automation


## Workflow 

<img width="829" height="340" alt="Screenshot 2026-08-14 at 18 31 51" src="https://github.com/user-attachments/assets/7511d29b-6554-423b-ab2d-5d80bfd772fd" />

The **Secure-CI** pipeline runs automatically on **pull requests** to the `main` and `staging` branches. It performs **five security-focused jobs:

1. **Docker Image Vulnerability Scan (Trivy)**
    
    - Scans the `bkimminich/juice-shop` image for known vulnerabilities.
        
2. **Secret Scanning (Trufflehog)**
    
    - Detects any exposed credentials, tokens, or API keys in the entire repository.
        
3. **Docker Image Configuration Check (Dockle)**
    
    - Flags misconfigurations and best-practice issues in the Docker image.
        
4. **SBOM Generation (Trivy)**
    
    - Creates a **Software Bill of Materials** for supply chain visibility and uploads it as a pipeline artifact. It also includes vulnerabilities found for later analysis. 
        
5. **Passive Web Application Scan (OWASP ZAP)**
    
    - Builds and runs the Dockerized app, then performs a **passive vulnerability scan**.

## Pipeline Testing
## Results
