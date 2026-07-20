🥗 Food Web App — End-to-End GitOps CI/CD Pipeline
A modern, production-ready DevOps pipeline for a containerized frontend web application. This project demonstrates continuous integration, security scanning, dynamic image tagging, and automated GitOps deployment to Amazon EKS using Jenkins and Argo CD.


[ Developer ]
     │
     │ 1. Push code
     ▼
┌───────────────────────────┐
│ Application Source Repo   │
│ (food-web-app)            │
└────────────┬──────────────┘
             │
             │ 2. Webhook trigger
             ▼
┌───────────────────────────────────────────────────────────┐
│ Jenkins CI Engine                                         │
│                                                           │
│  ├─ Clean Workspace                                       │
│  ├─ Checkout Code                                         │
│  ├─ SonarQube Analysis & Quality Gate                     │
│  ├─ Trivy File System Scan                                │
│  ├─ Docker Build & Push (Docker Hub)                      │
│  ├─ Trivy Container Image Scan                            │
│  └─ Update Manifests (Git commit image tag)              │
└────────────┬──────────────────────────────────────────────┘
             │
             │ 3. Push updated deployment.yaml
             ▼
┌───────────────────────────┐
│ K8s Manifest Repo         │
│ (food-app-k8s-manifests)  │
└────────────┬──────────────┘
             │
             │ 4. Auto-detect & Sync
             ▼
┌───────────────────────────┐        ┌───────────────────────────┐
│ Argo CD Controller        │───────►│ Amazon EKS Cluster        │
│ (GitOps Deployment)       │        │ (Pods, Services, Ingress) │
└───────────────────────────┘        └───────────────────────────┘ 


🛠️ Tech Stack & PrerequisitesCategoryTechnologyFrontendHTML5, CSS3, JavaScriptContainerizationDocker, Docker HubCI EngineJenkinsStatic Code & SecuritySonarQube, Trivy (FS & Image)GitOps & CDArgo CDCloud & OrchestrationAWS Elastic Kubernetes Service (EKS)NotificationsJenkins Email Extension
