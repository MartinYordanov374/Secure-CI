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
Besides the automated testing that the security tools listed below performed, I also included a fake AWS key from Canarytokens to test whether Trufflehog will catch them.

### Trivy Docker Image Scan
Trivy identified a large amount of vulnerabilities with their corresponding CVE and Severity. The image below shows a tiny part of the output.

<img width="1400" height="950" alt="Trivy_Scan" src="https://github.com/user-attachments/assets/a0e83ddd-e18f-4a31-8917-36f495a383c7" />

It is interesting to note that a majority of the vulnerabilities are within the dependencies of the scanned Docker image. Thus, there is not much that the developers using the image can do about that, other than update the dependencies where possible and applicable.

### Trufflehog Secrets Scan
Trufflehog successfully identified the canarytoken AWS key that I put in the repository, as shown below. As a result, the Trufflehog job failed.

<img width="1538" height="816" alt="Screenshot From 2026-08-14 17-21-09" src="https://github.com/user-attachments/assets/a4a99e06-a0c7-4296-80a8-0435e20b40d3" />

### Dockle Scan
Dockle identified a couple of interesting issues with the file as shown below.

<img width="2036" height="994" alt="DockleScan" src="https://github.com/user-attachments/assets/d209514b-a3e5-4603-a943-7423f2419ad0" />

Careful commentary about the findings is necessary. First and foremost, the FATAL issue is a false positive. None of the variables that Dockle detected are of sensitive nature.

Second, Dockle advises us to avoid using the *latest* image tag. This is smart because zero-day vulnerabilities could be introduced to the latest version of a Docker image, and it could take quite a while until they are detected and patched. This is why it is important to run Trivy in addition to such scans. Besides the obvious security issues that the *latest* tag introduces, it also opens the door to possible version mismatches and deployment issues.

The rest of the warnings that Dockle gives us are also important and follow best practices, but they are not as central to this project's goals as the outlined ones. Thus, no commentary is left for them.

### OWASP ZAP Passive Scan Results
The OWASP ZAP passive scan results in an artifact object, which includes the same data in three formats - Markdown, HTML, and JSON. The data concerns the issues that were identified and possible remediations. The image below shows the alerts that were raised during the scan, along with their risk level.

<img width="1440" height="371" alt="Screenshot From 2026-08-14 17-27-51" src="https://github.com/user-attachments/assets/c6834386-7e5c-4702-a014-88c95d1912ad" />

In addition to the alerts summary, there are also detailed alerts with solutions and references given, as shown in the two images below.

<img width="1420" height="262" alt="Screenshot 2026-08-15 at 1 09 45" src="https://github.com/user-attachments/assets/207198c1-e2d9-4574-a9b1-7af2e17772fc" />
<img width="1422" height="161" alt="Screenshot 2026-08-15 at 1 10 02" src="https://github.com/user-attachments/assets/85656856-ce59-46e5-b9a7-9400bf225854" />



