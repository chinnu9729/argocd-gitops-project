# GitOps Workflow using ArgoCD and Kubernetes

## Project Objective
Implement GitOps using ArgoCD to automatically synchronize Kubernetes
deployment resources from a GitHub repository.

## Tools Used
- AWS EC2
- Ubuntu 24.04
- K3s Kubernetes
- ArgoCD
- Git and GitHub
- Docker / Nginx

## Project Architecture
GitHub Repository -> ArgoCD -> Kubernetes -> Nginx Application

## Repository Structure
argocd-gitops-project/
├── manifests/
│   ├── deployment.yaml
│   └── service.yaml
└── README.md

## Deployment
ArgoCD monitors the manifests directory and automatically deploys
the Nginx application to the Kubernetes cluster.

## GitOps Workflow
1. Store Kubernetes manifests in GitHub.
2. Connect the repository to ArgoCD.
3. Enable automated synchronization.
4. Commit changes to GitHub.
5. ArgoCD detects changes and updates Kubernetes.

## Verification
kubectl get deployments -n gitops-demo
kubectl get pods -n gitops-demo
kubectl get services -n gitops-demo
