# 🧩 Kubernetes Deployment: React TODO App + NGINX with Ingress on AWS EC2

This project demonstrates how to deploy **two frontend apps** built with **React + Vite** (one served via NGINX, one as a TODO app) using **Docker**, **Kubernetes**, and **Ingress-NGINX** on an **AWS EC2** instance.

---

## 🧱 Project Files

| File | Description |
|------|-------------|
| `namespace.yaml` | Creates `project-1` namespace |
| `nginx-deployment.yaml` | Deployment for NGINX-hosted React app |
| `nginx-service.yaml` | Service for NGINX app |
| `todo-deployment.yaml` | Deployment for TODO React app |
| `todo-service.yaml` | Service for TODO app |
| `ingress.yaml` | Ingress rules for both apps |
| `config.yaml` | Helm config for Ingress-NGINX controller |

---

## 🚀 Step-by-Step Deployment Guide

### ✅ 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>


🛠️ 2. Create Kubernetes Namespace

kubectl apply -f namespace.yaml


📦 3. Deploy Both Applications


# Deploy TODO app
kubectl apply -f todo-deployment.yaml -n project-1
kubectl apply -f todo-service.yaml -n project-1

# Deploy NGINX-hosted app
kubectl apply -f nginx-deployment.yaml -n project-1
kubectl apply -f nginx-service.yaml -n project-1


🌐 4. Install Ingress 

kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/deploy-ingress-nginx.yaml



🔀 5. Apply Ingress Rules

kubectl apply -f ingress.yaml



🚪 Ingress Port Forwarding (for EC2 Access)
Use this command to forward EC2's port 8080 to Kubernetes ingress port 80:


sudo -E kubectl port-forward service/ingress-nginx-controller -n ingress-nginx 8080:80 --address=0.0.0.0




🌍 Access Your Apps in Browser


TODO App	http://<your-ec2-public-ip>:8080/todo
NGINX App	http://<your-ec2-public-ip>:8080/nginx
