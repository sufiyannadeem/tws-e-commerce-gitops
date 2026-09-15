EasyShop GitOps 🚀

GitOps repository for deploying and managing the EasyShop e-commerce application on Amazon EKS using Argo CD and Kubernetes manifests.

This repository follows the GitOps approach, where the desired Kubernetes state is stored in Git and Argo CD continuously synchronizes the cluster with the Git repository.

---

🏗️ Architecture

Developer
   │
   ▼
Application Repository
   │
   ▼
Jenkins CI Pipeline
   │
   ├── Run Tests
   ├── Trivy Security Scan
   ├── Docker Build
   └── Push Docker Image
          │
          ▼
     Docker Hub
          │
          ▼
   GitOps Repository
          │
          ▼
       Argo CD
          │
          ▼
     Amazon EKS
          │
          ▼
   NGINX Ingress
          │
          ▼
      HTTPS / TLS
          │
          ▼
       Users

---

📌 Project Overview

This repository contains the Kubernetes manifests required to deploy EasyShop to an Amazon EKS cluster.

The application deployment is managed using GitOps principles:

- Kubernetes configuration is stored in Git.
- Jenkins updates the application image version in the manifests.
- Argo CD detects changes in Git.
- Argo CD synchronizes the desired state with Amazon EKS.
- Kubernetes maintains the desired state inside the cluster.

---

📂 Repository Structure

.
├── namespace.yaml
├── configmap.yaml
├── secrets.yaml
├── deployment.yaml
├── service.yaml
├── ingress.yaml
├── mongodb.yaml
├── db-migration.yaml
├── hpa.yaml
└── README.md

«The exact files may vary depending on the current deployment configuration.»

---

☸️ Kubernetes Resources

The GitOps repository manages resources such as:

Resource| Purpose
Namespace| Isolates EasyShop resources
Deployment| Runs the application containers
Service| Provides internal Kubernetes networking
Ingress| Exposes the application externally
ConfigMap| Stores non-sensitive configuration
Secret| Stores sensitive configuration
HPA| Automatically scales application replicas
Database Migration Job| Performs database migrations
MongoDB| Application database

---

🔄 GitOps Deployment Flow

1. Developer pushes code

Application source code is pushed to GitHub.

2. Jenkins starts CI pipeline

Jenkins performs:

Clone
  ↓
Tests
  ↓
Trivy Security Scan
  ↓
Docker Build
  ↓
Docker Image Scan
  ↓
Push Image to Docker Hub

3. Jenkins updates GitOps repository

After successfully publishing the Docker image, Jenkins updates the Kubernetes manifest with the new image tag.

Example:

image: sufiyannadeem/easyshop-app:<IMAGE_TAG>

Jenkins commits the updated manifest back to this GitOps repository.

4. Argo CD detects the change

Argo CD continuously monitors this repository.

When a new commit is detected, Argo CD identifies the difference between:

Git Repository
     ↓
Desired State

and

Kubernetes Cluster
     ↓
Current State

5. Argo CD synchronizes EKS

Argo CD applies the required Kubernetes changes to the Amazon EKS cluster.

Git Change
    ↓
Argo CD
    ↓
Kubernetes Manifest
    ↓
EKS
    ↓
New Application Version

---

🔐 HTTPS / TLS

The application is exposed through Kubernetes Ingress.

TLS certificates are managed using cert-manager and Let's Encrypt.

User
  ↓
HTTPS
  ↓
NGINX Ingress
  ↓
EasyShop Service
  ↓
EasyShop Pods

Example host:

https://easyshop.nadeemsufiyan.in

---

📈 Autoscaling

The application uses Kubernetes Horizontal Pod Autoscaler (HPA) to automatically adjust the number of application replicas based on resource utilization.

Example:

Low Traffic
    ↓
Fewer Pods

High Traffic
    ↓
More Pods

---

🔍 Monitoring

The Kubernetes environment is monitored using:

- Prometheus
- Grafana
- Kubernetes metrics
- Application health checks

Monitoring helps track:

- CPU utilization
- Memory utilization
- Pod health
- Kubernetes resources
- Application availability

---

🛡️ Security

Security checks are integrated into the CI/CD pipeline using Trivy.

The pipeline scans:

Source / Dependencies
        ↓
Docker Image
        ↓
Security Vulnerability Detection

This helps identify known vulnerabilities before application images are deployed.

---

🔁 Continuous Delivery

The complete deployment workflow is:

Code
 ↓
GitHub
 ↓
Jenkins
 ↓
Automated Tests
 ↓
Trivy Security Scan
 ↓
Docker Build
 ↓
Docker Image Scan
 ↓
Docker Hub
 ↓
GitOps Repository
 ↓
Argo CD
 ↓
Amazon EKS
 ↓
NGINX Ingress
 ↓
HTTPS
 ↓
Users

---

🎯 GitOps Benefits

This deployment model provides:

- Version-controlled infrastructure
- Declarative Kubernetes configuration
- Automated deployments
- Auditability through Git history
- Easy rollback to previous versions
- Consistent cluster state
- Separation of CI and CD
- Reduced manual Kubernetes operations

---

🔙 Rollback

Because Kubernetes configuration is stored in Git, previous application versions can be recovered by reverting the corresponding Git commit.

Previous Git Commit
        ↓
Argo CD
        ↓
EKS
        ↓
Previous Application Version

This provides a simple and auditable rollback mechanism.

---

🧰 Technologies Used

Technology| Purpose
GitHub| Source and GitOps repository
Jenkins| CI automation
Docker| Containerization
Docker Hub| Container image registry
Kubernetes| Container orchestration
Amazon EKS| Managed Kubernetes cluster
Argo CD| GitOps continuous delivery
NGINX Ingress| Application ingress
cert-manager| TLS certificate management
Let's Encrypt| TLS certificates
Terraform| Infrastructure provisioning
Trivy| Security scanning
Prometheus| Metrics collection
Grafana| Monitoring and visualization

---

👨‍💻 Project

EasyShop – Cloud Native E-Commerce Deployment

The project demonstrates a production-style DevOps workflow combining:

- AWS
- Terraform
- Docker
- Jenkins
- Kubernetes
- Amazon EKS
- Argo CD
- GitOps
- NGINX Ingress
- cert-manager
- Prometheus
- Grafana
- Trivy

---

📜 License

This project is intended for learning and demonstration purposes.
