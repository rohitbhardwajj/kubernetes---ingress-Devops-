# 🧩 Kubernetes React + TODO App with NGINX and Ingress

This project deploys two frontend apps (`nginx` + `todo`) using **React** and **Vite**, containerized with **Docker**, and deployed to **Kubernetes** on **AWS EC2** using **Ingress-NGINX** for routing.

---

## 📁 Folder Structure



├── config.yaml # Ingress NGINX Controller Helm config
├── ingress.yaml # Ingress rule for both apps
├── namespace.yaml # Creates project-1 namespace
├── nginx-deployment.yaml # React frontend (nginx served) deployment
├── nginx-service.yaml # Service for frontend app
├── todo-deployment.yaml # TODO app deployment
├── todo-service.yaml # Service for todo app



---

## 🚀 Deployment Steps

### 1️⃣ Create Namespace
```bash
kubectl apply -f namespace.yaml


kubectl apply -f nginx-deployment.yaml -n project-1
kubectl apply -f nginx-service.yaml -n project-1

kubectl apply -f todo-deployment.yaml -n project-1
kubectl apply -f todo-service.yaml -n project-1



helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx -f config.yaml -n ingress-nginx --create-namespace


kubectl apply -f ingress.yaml



🚪 Ingress Port Forwarding for EC2 Access
To access your app via Ingress NGINX from your EC2 instance's public IP, use the following command:


sudo -E kubectl port-forward service/ingress-nginx-controller -n ingress-nginx 8080:80 --address=0.0.0.0


🌐 Now Access Your App:
Open this in your browser:


http://<your-ec2-public-ip>:8080/todo      for accessing todo-app
http://<your-ec2-public-ip>:8080/nginx      for accessing nginx-app
