# MVP (Minimum Viable Product)

## Overview
The Minimum Viable Product (MVP) for the AsciiArtify project aims to deploy a basic application using ArgoCD, which tracks changes from the GitHub repository [go-demo-app](https://github.com/den-vasyliev/go-demo-app) and automatically synchronizes them onto a Kubernetes cluster.

## Steps to Set Up MVP

### 1. Set Up Kubernetes Cluster with k3d
- Use k3d to create a Kubernetes cluster locally.
- Ensure that the cluster is up and running.
```bash
  k3d cluster create demo
  kubectl cluster-info
```

### 2. Install ArgoCD
- Follow the official ArgoCD documentation to install ArgoCD on the Kubernetes cluster.
- Verify that ArgoCD pods are running successfully.
```bash
  kubectl create namespace argocd
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 3. Configure Application in ArgoCD
- Download Argo CD CLI
- Add the go-demo-app repository to ArgoCD for continuous delivery.
- Configure automatic synchronization of changes from the repository to the Kubernetes cluster.
More detailed installation instructions can be found via the [CLI installation documentation.](https://argo-cd.readthedocs.io/en/stable/cli_installation/ "CLI installation documentation.").
```bash
  kubectl config set-context --current --namespace=argocd
  argocd login --core
  argocd app create demo --repo https://github.com/den-vasyliev/go-demo-app.git --path helm  --dest-server https://kubernetes.default.svc --dest-namespace demo
```

### 4. Demonstrate Application Deployment
- Deploy the go-demo-app using ArgoCD onto the Kubernetes cluster.
- Monitor the synchronization process and ensure successful deployment of the application.
```bash
  argocd app get demo
  argocd app sync demo
```

## Demo Instructions

### Accessing ArgoCD UI
- Use port-forwarding to access the ArgoCD UI:
```bash
  argocd admin initial-password -n argocd
  kubectl port-forward svc/argocd-server -n argocd 8080:443
```

### Accessing ArgoCD UI
- Open a web browser and navigate to [https://localhost:8080](https://localhost:8080) to access the ArgoCD UI.

### Monitoring Application Deployment
- Navigate to the ArgoCD UI and observe the deployment status of the go-demo-app.
- Verify that changes from the GitHub repository are automatically synchronized and deployed onto the Kubernetes cluster.

## Conclusion
The MVP demonstrates the automated deployment of the go-demo-app using ArgoCD on a Kubernetes cluster provisioned with k3d. This setup enables the AsciiArtify team to efficiently manage application deployments and iterate on features based on user feedback.
