# 🚀 Argo CD Demo Deployment

This project demonstrates how to deploy a simple **nginx** application to a Kubernetes cluster using **Argo CD** in a GitOps workflow.

---

## ✅ Prerequisites

Make sure you have the following installed and configured:

- A Kubernetes cluster (Minikube, Kind, EKS, GKE, etc.)
- `kubectl` installed and configured
- `argocd` CLI installed
- GitHub repository with this code pushed

---

 📦 Step 1: Clone and Push the Repository

```bash
git clone https://github.com/<your-username>/argo-cd.git
cd argo-cd
git add .
git commit -m "Initial commit for Argo CD demo"
git push origin main

🛠️ Step 2: Install Argo CD in Your Cluster
Create Argo CD namespace:

kubectl create namespace argocd

Install Argo CD components:
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

🌐 Step 3: Access the Argo CD UI
Port-forward Argo CD API server:
kubectl port-forward svc/argocd-server -n argocd 8080:443

Open your browser and go to:
https://localhost:8080

🔐 Step 4: Login via Argo CD CLI
argocd login localhost:8080

🚀 Step 5: Create Your Application in Argo CD:
argocd app create argo-demo \
  --repo https://github.com/<your-username>/argo-cd.git \
  --path . \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace argo-demo

🔄 Step 6: Sync the Application:
argocd app sync argo-demo
This will deploy your application to the Kubernetes cluster.

🛠 Making Changes
If you make changes to any of the following files:

deployment.yaml

service.yaml

namespace.yaml

Push the changes to GitHub, then run the sync command:
argocd app sync argo-demo.

This ensures Argo CD updates your cluster to reflect the latest state defined in Git.