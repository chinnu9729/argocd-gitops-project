# GitOps Workflow Using ArgoCD and Kubernetes

## Project Overview

Implemented an automated GitOps deployment workflow using ArgoCD, Kubernetes (K3s), AWS EC2, and GitHub. The project demonstrates how Kubernetes application configurations can be maintained in Git and automatically synchronized to a Kubernetes cluster using ArgoCD.

## Project Objectives

- Implement GitOps principles using ArgoCD.
- Deploy a containerized Nginx application on Kubernetes.
- Integrate a GitHub repository with ArgoCD.
- Enable automatic synchronization of Kubernetes manifests.
- Demonstrate automated application scaling through Git commits.
- Verify application availability and cluster state.

## Technologies Used

| Technology | Purpose |
|---|---|
| AWS EC2 | Cloud infrastructure |
| Ubuntu 24.04 | Operating system |
| K3s | Lightweight Kubernetes cluster |
| Kubernetes | Container orchestration |
| ArgoCD | GitOps continuous delivery |
| Git | Version control |
| GitHub | Source code repository |
| Docker | Container technology |
| Nginx | Sample web application |

## Architecture

```text
       Developer
           |
           | Git commit / push
           v
     GitHub Repository
           |
           | Monitors manifests/
           v
         ArgoCD
           |
           | Automatic Sync
           v
     K3s Kubernetes Cluster
           |
           v
      gitops-demo Namespace
           |
      Nginx Deployment
           |
        ReplicaSet
           |
      3 Nginx Pods
           |
      Nginx Service
```

## Repository Structure

```text
argocd-gitops-project/
│
├── manifests/
│   ├── deployment.yaml
│   └── service.yaml
│
└── README.md
```

## Infrastructure Setup

- Created an Ubuntu 24.04 EC2 instance on AWS.
- Installed and configured K3s Kubernetes.
- Configured kubectl access to the Kubernetes cluster.
- Installed ArgoCD in the `argocd` namespace.
- Accessed the ArgoCD dashboard through the configured EC2 service endpoint.

## Kubernetes Configuration

### Deployment

The `deployment.yaml` manifest defines an Nginx application with three replicas.

- Deployment name: `nginx-app`
- Namespace: `gitops-demo`
- Container image: `nginx:1.27-alpine`
- Desired replicas: 3
- Container port: 80

### Service

The `service.yaml` manifest creates a ClusterIP service.

- Service name: `nginx-service`
- Service type: ClusterIP
- Port: 80
- Target port: 80

## ArgoCD Configuration

Created an ArgoCD application with the following configuration:

| Setting | Value |
|---|---|
| Application Name | nginx-gitops |
| Project | default |
| Repository | https://github.com/chinnu9729/argocd-gitops-project.git |
| Branch | main |
| Manifest Path | manifests |
| Destination | https://kubernetes.default.svc |
| Namespace | gitops-demo |
| Sync Policy | Automatic |
| Auto-Sync | Enabled |
| Self-Heal | Enabled |
| Prune Resources | Enabled |

## GitOps Workflow

1. Created Kubernetes Deployment and Service manifests.
2. Pushed the manifests to the GitHub repository.
3. Connected the repository to ArgoCD.
4. Configured the ArgoCD application to monitor the `main` branch and `manifests` directory.
5. Enabled automatic synchronization.
6. Updated the Deployment replica count from 2 to 3 in GitHub.
7. Pushed the updated manifest to the repository.
8. ArgoCD detected the new commit and automatically synchronized the Kubernetes cluster.
9. Kubernetes created the third Nginx Pod.

## GitOps Scaling Demonstration

Initial configuration:

```yaml
spec:
  replicas: 2
```

Updated configuration:

```yaml
spec:
  replicas: 3
```

Git commit:

`aaf0442` – Scale nginx deployment to three replicas

GitHub repository:

https://github.com/chinnu9729/argocd-gitops-project

ArgoCD successfully synchronized the new configuration, and Kubernetes reached the desired state of three running replicas.

## Verification Commands

Check Kubernetes nodes:

```bash
kubectl get nodes
```

Check the deployment:

```bash
kubectl get deployments -n gitops-demo
```

Check the Pods:

```bash
kubectl get pods -n gitops-demo
```

Check the Service:

```bash
kubectl get services -n gitops-demo
```

Expected deployment status:

```text
NAME        READY   UP-TO-DATE   AVAILABLE
nginx-app   3/3     3            3
```

Expected Pod status: Three Nginx Pods in `Running` state with `1/1` containers ready.

## Restart Verification

After restarting the EC2 instance:

- Reconnected through EC2 Instance Connect.
- Restored kubectl configuration.
- Verified the Git repository was up to date.
- Confirmed that all three Nginx Pods were still running.

## Project Results

- Successfully deployed Nginx on Kubernetes using ArgoCD.
- Integrated GitHub with ArgoCD for GitOps-based delivery.
- Implemented automatic synchronization of Kubernetes manifests.
- Demonstrated automatic scaling from two to three replicas through a Git commit.
- Verified the deployment status as 3/3 Ready.
- Confirmed application resources remained available after an EC2 restart.

## Screenshots

Project evidence to be added in the `screenshots/` directory:

1. ArgoCD application showing Healthy and Synced.
2. ArgoCD application resource tree showing three Pods.
3. GitHub Deployment manifest showing three replicas.
4. GitHub commit history showing the scaling update.
5. EC2 terminal showing the three running Pods.

## Author

**Vancha Rishika Reddy**

GitHub: https://github.com/chinnu9729

Project Repository: https://github.com/chinnu9729/argocd-gitops-project
