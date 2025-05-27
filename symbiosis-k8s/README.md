# Symbiosis Kubernetes Project

This project containerizes and deploys the [Node.js CRUD App](https://github.com/chapagain/nodejs-mysql-crud) with MySQL using Kubernetes on Minikube or any K8s cluster.

## Features
- MySQL with Persistent Volume
- Node.js backend
- Horizontal Pod Autoscaler
- Liveness/Readiness Probes
- CI/CD with GitHub Actions
- Monitoring via Prometheus annotations

### 1. Minikube setup
Prequisite:
Install Docker, Minikube, Kubectl
Start Docker
minikube start
minikube status

### 2. Docker Build & Push
clone project reposiotry: git clone https://github.com/chapagain/nodejs-mysql-crud

create a Dockerfile to create container images

docker build -t <your-dockerhub>/nodejs-mysql-crud-app:latest .

Login docker registory before image push
docker login -u username -p password
docker push <your-dockerhub>/nodejs-mysql-crud-app:latest

Run below command to test the container:

docker run -p 3000:3000 nodejs-mysql-crud-app
It should show the below message.
Server running at port 3000: http://127.0.0.1:3000

3. Kubernetes Setup
create the following file under k8s/manifests

symbiosis-k8s/
├── Dockerfile
├── README.md
└── nodejs-mysql-crud/
└── manifests/
├── node-deployment.yaml
├── mysql-deployment.yaml
├── service.yaml
├── ingress.yaml
├── hpa.yaml
├── pv.yaml
├── pvc.yaml
├── configmap.yaml
└── secret.yaml



kubectl apply -f manifests/

need to configure DNS (e.g., /etc/hosts) with:
127.0.0.1 crud-app.local

Ensure NGINX Ingress Controller is installed in Minikube:
minikube addons enable ingress

4. View the App

minikube service node-service
5. Monitoring & Scaling
HPA automatically scales based on CPU usage.

Liveness and readiness probes ensure uptime.

GitHub Actions CD
Push to main will trigger deployment via GitHub Actions (.github/workflows/deploy.yml).
