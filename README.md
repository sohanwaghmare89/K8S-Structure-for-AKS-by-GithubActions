# 🚀 AKS Application Deployment Structure using GitHub Actions

## 📖 Overview

This repository provides a standardized Kubernetes deployment structure for applications running on **Azure Kubernetes Service (AKS)** using **GitHub Actions** for Continuous Integration and Continuous Deployment (CI/CD).

The objective is to establish a reusable and scalable deployment framework that enables teams to:

* Automate application deployments
* Maintain environment consistency
* Follow Kubernetes best practices
* Reduce manual deployment efforts
* Improve release reliability and speed

This structure can be adopted across multiple projects to ensure a consistent deployment approach for AKS workloads.

---

## 🏗️ Architecture

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
GitHub Actions Workflow
    │
    ├── Code Validation
    ├── Build Docker Image
    ├── Push Image to ACR
    ├── Update Kubernetes Manifests
    └── Deploy to AKS
             │
             ▼
 Azure Kubernetes Service (AKS)
```

---

## 📂 Repository Structure

```bash
.
├── .github/
│   └── workflows/
│       ├── dev-deploy.yml
│       ├── qa-deploy.yml
│       ├── uat-deploy.yml
│       └── prod-deploy.yml
│
├── kubernetes/
│   ├── dev/
│   ├── qa/
│   ├── uat/
│   └── prod/
│
├── manifests/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── configmap.yaml
│   └── secret.yaml
│
├── scripts/
│   └── deployment.sh
│
└── README.md
```

---

## ⚙️ CI/CD Workflow

### 1️⃣ Code Commit

Developers push code changes to the GitHub repository.

### 2️⃣ Workflow Trigger

GitHub Actions automatically triggers based on the configured branch strategy.

### 3️⃣ Build Stage

* Checkout Source Code
* Validate Kubernetes Manifests
* Build Docker Image
* Tag Image Version

### 4️⃣ Image Push

Container images are pushed to:

* Azure Container Registry (ACR)
* Docker Hub (Optional)

### 5️⃣ Deployment Stage

The workflow:

* Authenticates with Azure
* Connects to AKS Cluster
* Updates Kubernetes Resources
* Performs Rolling Deployment

### 6️⃣ Verification

Deployment validation includes:

* Pod Health Checks
* Rollout Verification
* Application Availability Validation

---

## 🌍 Environment Strategy

| Environment | Purpose                       |
| ----------- | ----------------------------- |
| Dev         | Development & Feature Testing |
| QA          | Quality Assurance Testing     |
| UAT         | User Acceptance Testing       |
| Prod        | Production Workloads          |

Each environment contains its own Kubernetes configuration and deployment settings.

---

## 🔐 Required GitHub Secrets

Configure the following repository secrets:

```text
AZURE_CLIENT_ID
AZURE_CLIENT_SECRET
AZURE_TENANT_ID
AZURE_SUBSCRIPTION_ID
AKS_CLUSTER_NAME
AKS_RESOURCE_GROUP
ACR_NAME
```

---

## ☸️ Kubernetes Resources

### Deployment

Manages application lifecycle, scaling, and rolling updates.

### Service

Provides internal and external access to application pods.

### Ingress

Handles HTTP/HTTPS routing and SSL termination.

### ConfigMap

Stores non-sensitive application configuration.

### Secret

Stores sensitive application data securely.

### Namespace

Provides logical separation between environments.

---

## ✨ Key Features

* GitHub Actions based CI/CD
* AKS Native Deployment Support
* Environment-wise Configuration
* Docker Image Versioning
* Automated Rollout Deployment
* Kubernetes Best Practices
* Namespace Isolation
* ConfigMap & Secret Management
* Scalable Deployment Structure
* Easy Rollback Capability

---

## 🚀 Deployment Commands

### Verify Pods

```bash
kubectl get pods -A
```

### Verify Services

```bash
kubectl get svc -A
```

### Verify Ingress

```bash
kubectl get ingress -A
```

### Check Rollout Status

```bash
kubectl rollout status deployment/<deployment-name> -n <namespace>
```

### View Logs

```bash
kubectl logs -f <pod-name> -n <namespace>
```

---

## 📌 Best Practices

✅ Use separate namespaces per environment

✅ Store sensitive information in Kubernetes Secrets

✅ Use resource requests and limits

✅ Implement readiness and liveness probes

✅ Follow Pull Request based deployments

✅ Use image tags instead of latest

✅ Enable deployment approval for production

✅ Maintain environment-specific configuration

---

## 🎯 Benefits

* Faster Application Delivery
* Reduced Manual Effort
* Improved Deployment Reliability
* Standardized AKS Structure
* Better Environment Management
* Enhanced Security
* Scalable Architecture
* Simplified Operations

---

## 🏁 Conclusion

This repository serves as a reusable Kubernetes deployment framework for Azure Kubernetes Service (AKS). By leveraging GitHub Actions, teams can automate application delivery, enforce deployment standards, and maintain a scalable and reliable CI/CD process across multiple environments.
