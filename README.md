# DevSecOps Secure CI Pipeline
This project demonstrates a **secure CI pipeline** for Dockerized applications using **DevSecOps principles**. The pipeline integrates **security scanning, secret detection, and compliance checks** directly into the CI workflow to prevent vulnerabilities from reaching production-level code.

The pipeline was tested against the **OWASP Juice Shop**, a deliberately vulnerable web application, making it an excellent environment for experimenting **real-world vulnerability scanning and secret detection** in a safe context.

For a deep dive into the project, <a href='https://medium.com/@martin.yordanov.official/devsecops-building-a-secure-ci-pipeline-7915f040ca94'>check out my Medium article.</a>
## Table of Contents

1. [The motivation behind the project](#the-motivation-behind-the-project)
2. [What I strived to achieve and learn through this project](#what-i-strived-to-achieve-and-learn-through-this-project)
3. [Tech Stack](#tech-stack)
4. [Workflow](#workflow)
5. [Pipeline Testing and Results](#Pipeline-Testing-And-Results)

## The motivation behind the project
No learning journey is linear, and this project is not an exception. While exploring cybersecurity, and in particular security engineering, I came across DevSecOps and security pipelines. 

I was already aware of DevOps principles, but I had not paid much attention to Dev**Sec**Ops, so this project was the perfect way to gain hands-on experience in DevSecOps practices and building security pipelines.

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
<img width="699" height="491" alt="Screenshot 2026-08-14 at 20 03 29" src="https://github.com/user-attachments/assets/ed0dcc04-3eb1-45d7-8755-df203f25a029" />

The **Secure-CI** pipeline runs automatically on **pull requests** to the `main` and `staging` branches. It performs five security-focused jobs:

1. **Docker Image Vulnerability Scan (Trivy)**
    
    - Scans the `bkimminich/juice-shop` image for known vulnerabilities and presents them in table format. 
        
2. **Secret Scanning (Trufflehog)**
    
    - Detects any exposed credentials, tokens, or API keys in the entire repository.
        
3. **Docker Image Configuration Check (Dockle)**
    
    - Flags misconfigurations and best-practice issues in the Docker image.
        
4. **SBOM Generation (Trivy)**
    
    - Creates a **Software Bill of Materials** for supply chain visibility and uploads it as a pipeline artifact. It also includes vulnerabilities found for later analysis. 
        
5. **Passive Web Application Scan (OWASP ZAP)**
    
    - Builds and runs the Dockerized app, then performs a **passive vulnerability scan**.


## Pipeline Testing and Results
### Trivy Docker Image Scan
<img width="1400" height="950" alt="Trivy_Scan" src="https://github.com/user-attachments/assets/a0e83ddd-e18f-4a31-8917-36f495a383c7" />

### Trufflehog Secrets Scan
<img width="1538" height="816" alt="Screenshot From 2026-08-14 17-21-09" src="https://github.com/user-attachments/assets/a4a99e06-a0c7-4296-80a8-0435e20b40d3" />

### Dockle Scan
<img width="2036" height="994" alt="DockleScan" src="https://github.com/user-attachments/assets/d209514b-a3e5-4603-a943-7423f2419ad0" />

### OWASP ZAP Passive Scan Results
<img width="1913" height="215" alt="Screenshot From 2026-08-14 17-29-39" src="https://github.com/user-attachments/assets/9623faa0-3068-4c87-92ba-9495820e02f3" />

<img width="1440" height="371" alt="Screenshot From 2026-08-14 17-27-51" src="https://github.com/user-attachments/assets/c6834386-7e5c-4702-a014-88c95d1912ad" />

