EasyShop GitOps 🚀

This repository contains the Kubernetes manifests and deployment configuration for the EasyShop application.

It is used as the GitOps repository for managing application deployments to Amazon EKS using Argo CD.

🔄 GitOps Workflow

Jenkins
   ↓
Build & Push Docker Image
   ↓
Update Kubernetes Manifests
   ↓
GitOps Repository
   ↓
Argo CD
   ↓
Amazon EKS

📂 Repository Contents

This repository contains Kubernetes configuration files such as:

- Deployments
- Services
- Ingress
- ConfigMaps
- Secrets
- HPA
- Database migration jobs
- Other Kubernetes resources required by the application

🚀 Deployment

Argo CD monitors this repository and synchronizes changes to the Kubernetes cluster.

Any changes to the Kubernetes manifests can therefore be tracked through Git history and deployed through the GitOps workflow.

🔗 Main Application Repository

For the application source code, CI/CD pipeline, Docker configuration, security scanning, monitoring, and complete project documentation, refer to the main EasyShop repository.

---

GitOps Repository: Kubernetes deployment configuration
Deployment Tool: Argo CD
Platform: Amazon EKS

---

📜 License

This project is intended for learning and demonstration purposes.
