# Production-Grade EKS Platform with GitOps & Observability

## 📌 Overview
This repository demonstrates a **production-grade Kubernetes platform on AWS EKS** built using modern DevOps and SRE practices.

The project focuses on:
- Infrastructure provisioning using **Terraform**
- **GitOps-based deployments** using Argo CD
- Scalable ingress with **AWS Application Load Balancer**
- **Observability-first design** using Prometheus and Grafana

This setup closely resembles how real-world enterprise platforms are built and operated.

---

## 🏗️ High-Level Architecture Diagram

```
                 +----------------------+
                 |        GitHub        |
                 | (Desired State Repo) |
                 +----------+-----------+
                            |
                            | GitOps Sync
                            v
+-------------+     +--------------------+
|  Developer  | --> |      Argo CD       |
+-------------+     +---------+----------+
                               |
                               | Applies Manifests
                               v
              +-----------------------------------+
              |            AWS EKS               |
              |                                   |
              |  +-------------+   +-----------+ |
              |  | Application |<->|  Service  | |
              |  |    Pods     |   +-----------+ |
              |        |                     |   |
              |        v                     |   |
              |     ALB Ingress --------------+   |
              +-----------------------------------+
                               |
                               v
                         +-----------+
                         |  Users    |
                         +-----------+

      +------------------------------------------------+
      | Prometheus scrapes metrics from the cluster    |
      | Grafana visualizes metrics & dashboards        |
      +------------------------------------------------+
```

---

## 🔁 End-to-End Flow

1. Terraform provisions AWS infrastructure (VPC + EKS).
2. Argo CD watches this GitHub repository.
3. Kubernetes manifests are auto-synced to the cluster.
4. Traffic is routed via AWS ALB Ingress.
5. Prometheus collects metrics.
6. Grafana visualizes metrics.

---

## 📂 Repository Structure

```
eks-gitops-platform/
├── terraform/
│   ├── provider.tf
│   ├── main.tf
│   ├── vpc.tf
│   ├── eks.tf
│   ├── variables.tf
│   └── outputs.tf
├── argocd/
│   └── application.yaml
├── kubernetes/
│   ├── sample-app.yaml
│   ├── demo-service.yaml
│   └── ingress.yaml
├── monitoring/
│   ├── prometheus.yaml
│   └── grafana.yaml
└── README.md
```

---

## ▶️ How to Run

### Prerequisites
- AWS account
- AWS CLI
- Terraform >= 1.4
- kubectl

### Provision Infrastructure
```bash
cd terraform
terraform init
terraform apply
```

### Configure kubectl
```bash
aws eks update-kubeconfig --region us-east-1 --name prod-eks-gitops
```

### Install Argo CD
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Deploy via GitOps
```bash
kubectl apply -f argocd/application.yaml
```

---

## 🧠 Interview Summary
This project showcases real-world Kubernetes platform engineering using Terraform, GitOps, ingress, and observability.
