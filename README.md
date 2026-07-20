# 🥗 Food Web App — End-to-End GitOps CI/CD Pipeline

![GitOps](https://img.shields.io/badge/GitOps-ArgoCD-orange)
![Kubernetes](https://img.shields.io/badge/Kubernetes-EKS-blue)
![Jenkins](https://img.shields.io/badge/CI%2FCD-Jenkins-red)
![Docker](https://img.shields.io/badge/Container-Docker-blue)
![Terraform](https://img.shields.io/badge/IaC-Terraform-purple)

## 📌 Project Overview

This project demonstrates a **production-style DevOps workflow** for deploying a containerized Food Web Application using a complete **CI/CD + GitOps architecture**.

The pipeline automates the entire software delivery lifecycle:

- Source code management using GitHub
- Continuous Integration using Jenkins
- Static code analysis using SonarQube
- Security vulnerability scanning using Trivy
- Docker image creation and publishing
- Kubernetes deployment on Amazon EKS
- Automated application delivery using Argo CD GitOps

The goal of this project is to implement a scalable, secure, and automated deployment workflow similar to real-world enterprise environments.

---

# 🏗️ Architecture Overview

                     Developer
                         |
                         |
                Push Application Code
                         |
                         ▼
          ┌─────────────────────────┐
          │  GitHub Application Repo │
          │     (food-web-app)       │
          └────────────┬────────────┘
                       |
                       |
                Webhook Trigger
                       |
                       ▼
          ┌──────────────────────────┐
          │       Jenkins CI          │
          │                          │
          │  1. Checkout Code        │
          │  2. SonarQube Analysis    │
          │  3. Quality Gate          │
          │  4. Trivy FS Scan         │
          │  5. Docker Build         │
          │  6. Push Docker Image    │
          │  7. Trivy Image Scan     │
          │  8. Update K8s Manifest  │
          └────────────┬─────────────┘
                       |
                       |
                Commit Image Tag
                       |
                       ▼
          ┌─────────────────────────┐
          │ Kubernetes Manifest Repo │
          │  (food-app-k8s-manifests)│
          └────────────┬────────────┘
                       |
                       |
              GitOps Synchronization
                       |
                       ▼
          ┌─────────────────────────┐
          │        Argo CD           │
          │ Continuous Deployment    │
          └────────────┬────────────┘
                       |
                       |
                       ▼
          ┌─────────────────────────┐
          │      Amazon EKS          │
          │                          │
          │ Kubernetes Resources     │
          │ - Deployment             │
          │ - Service                │
          │ - Ingress                │
          │ - Pods                   │
          └─────────────────────────┘

          
---

# 🚀 Tech Stack

## Application

| Component | Technology |
|-----------|------------|
| Frontend | HTML / CSS / JavaScript |
| Web Server | Nginx |
| Containerization | Docker |

---

## DevOps Tools

| Category | Tools |
|----------|-------|
| Source Control | GitHub |
| CI/CD | Jenkins |
| Code Quality | SonarQube |
| Security Scanner | Trivy |
| Container Registry | Docker Hub |
| Container Platform | Kubernetes |
| Cloud Platform | AWS |
| Kubernetes Service | Amazon EKS |
| GitOps | Argo CD |
| Infrastructure as Code | Terraform |
| Package Manager | Helm |

---

# 🔄 CI/CD Pipeline Workflow

## 1. Developer Code Push

Developer pushes application changes into the GitHub repository.

Example:
git add .
git commit -m "Updated food application"
git push origin main 


GitHub webhook triggers Jenkins automatically.

---

# 2. Jenkins Continuous Integration

Jenkins performs the following stages:

## Stage 1: Clean Workspace

Removes previous build artifacts.

cleanWs()


---

## Stage 2: Source Code Checkout

Jenkins pulls the latest application code.

GitHub Repository
|
▼
Jenkins


---

## Stage 3: SonarQube Code Analysis

Performs:

- Code quality analysis
- Bug detection
- Code smell detection
- Maintainability checks


Pipeline:

Application Code
|
▼
Sonar Scanner
|
▼
SonarQube Server

---

## Stage 4: Quality Gate Validation

Pipeline continues only if the application passes SonarQube quality standards.

Example:


Quality Gate Passed
|
▼
Continue Pipeline


---

## Stage 5: Trivy File System Scan

Scans source code for vulnerabilities.

Checks:

- Dependency vulnerabilities
- Security issues
- Misconfigurations


Example:
trivy fs .


---

## Stage 6: Docker Image Build

Jenkins creates a container image.

Example:
docker build
-t thanuesh13/food-app:${BUILD_NUMBER} .


---

## Stage 7: Push Image to Docker Hub

Generated image is pushed to Docker registry.

Example:
docker push thanuesh13/food-app:${BUILD_NUMBER}


---

## Stage 8: Container Image Security Scan

Trivy scans the Docker image.

Example:


trivy image thanuesh13/food-app:${BUILD_NUMBER}


---

## Stage 9: Update Kubernetes Manifest

Jenkins updates the image version inside Kubernetes deployment YAML.

Before:

```yaml
image:
  thanuesh13/food-app:10

After:

image:
  thanuesh13/food-app:11

Then Jenkins commits the change.

git commit -m "Update image version"
git push

🔁 GitOps Continuous Deployment
Argo CD Workflow

Argo CD continuously monitors the Kubernetes manifest repository.

Manifest Repository
          |
          |
          ▼
       Argo CD
          |
          |
          ▼
      Amazon EKS

When Jenkins updates the image tag:

Argo CD detects Git changes
Compares desired state with cluster state
Synchronizes automatically
Deploys the latest application version
