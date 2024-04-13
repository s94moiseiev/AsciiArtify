# Create demo codespace

Creating a demo Codespace on GitHub is a great way to showcase your project's development environment and enable collaborators to quickly spin up a development environment without needing to set up anything locally. Here's a step-by-step guide to create a demo Codespace on GitHub:

[![Create demo codespace](https://i9.ytimg.com/vi_webp/aSisX3BOG9k/mq1.webp?sqp=CJi36rAG&rs=AOn4CLBglom1JD5a4f6d8NQicBPHjPZBfg "Create demo codespace")](https://youtu.be/aSisX3BOG9k "Create demo codespace")

# Set Up Kubernetes Cluster

We will use k3d to create a demo Kubernetes cluster.
k3d is a lightweight wrapper to run k3s (Rancher Lab’s minimal Kubernetes distribution) in docker.

[![Set Up Kubernetes Cluster](https://i9.ytimg.com/vi/NiqSyFp_Zl8/mq1.jpg?sqp=CJy-6rAG&rs=AOn4CLD0aIhMM53PB2LrBL1aVLwUJVJZ6A&retry=4 "Set Up Kubernetes Cluster")](https://youtu.be/NiqSyFp_Zl8 "Set Up Kubernetes Cluster")

# Install ArgoCD

We will use official ArgoCD documentation to install ArgoCD on the Kubernetes cluster.

[![asciicast](https://asciinema.org/a/VkjMXqSC2x2RkzheH6OGipAUu.svg)](https://asciinema.org/a/VkjMXqSC2x2RkzheH6OGipAUu)

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Access ArgoCD CLI/UI

We can use the following options to work with ArgoCD:

### CLI

Must be installed Argo CD CLI.
More detailed installation instructions can be found via the [CLI installation documentation.](https://argo-cd.readthedocs.io/en/stable/cli_installation/ "CLI installation documentation.")

[![asciicast](https://asciinema.org/a/0AViQNtaLEMEEfaxJosG6rKKX.svg)](https://asciinema.org/a/0AViQNtaLEMEEfaxJosG6rKKX)

```bash
argocd login --core
kubectl config set-context --current --namespace=argocd
kubectl config get-contexts -o name
```
### UI

We will use port-forwarding to demonstrate the web interface.

```bash
kubectl port-forward svc/argocd-server -n argocd 8443:443
```
[![ArgoCD UI](https://i9.ytimg.com/vi_webp/k3eYUsL3OBU/mq2.webp?sqp=CKjT6rAG&rs=AOn4CLDLh0yeacpx4RbhSzD3lo9lYYCkDQ "ArgoCD UI")](https://youtu.be/k3eYUsL3OBU "ArgoCD UI")

After that, go to the ports section and click on the port 8443 to open in the browser.

## Demonstrate Basic Functionality

Let's create a demo application by taking it [from the documentation](https://argo-cd.readthedocs.io/en/stable/getting_started/#6-create-an-application-from-a-git-repository "from the documentation")

[![Demonstrate Basic Functionality](https://i9.ytimg.com/vi_webp/jPQEpqUxns8/mq1.webp?sqp=CNTV6rAG&rs=AOn4CLAZr8e-5RSlkkTNJFaxDaHd7p8qAQ "Demonstrate Basic Functionality")](https://youtu.be/jPQEpqUxns8 "Demonstrate Basic Functionality")

# Conclusions

In this Proof of Concept (PoC), we successfully demonstrated the deployment of ArgoCD on a Kubernetes cluster using k3d. We followed a structured approach to set up the environment and provided clear instructions for accessing both the ArgoCD CLI and UI.
