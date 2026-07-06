# Python Flask Task Manager - GitOps with Argo CD

## Project Overview

This project demonstrates a complete GitOps workflow using:

- Python Flask
- Docker
- Kubernetes (Kind)
- GitHub
- Argo CD

Whenever a Kubernetes manifest is updated and pushed to GitHub, Argo CD automatically synchronizes the Kubernetes cluster.

---

## Architecture

Developer
↓
Git Push
↓
GitHub
↓
Argo CD
↓
Kubernetes
↓
Application

---

## Project Structure

TaskManager/
│
├── app.py
├── Dockerfile
├── requirements.txt
├── templates/
├── static/
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
└── README.md

---

## Prerequisites

- Python
- Docker Desktop
- kubectl
- Kind
- Git
- Argo CD

---

## Build Docker Image

docker build -t task-manager:v1 .

---

## Create Kind Cluster

kind create cluster --name first-cluster --config kind-config.yaml

---

## Load Docker Image

kind load docker-image task-manager:v1 --name first-cluster

---

## Deploy to Kubernetes

kubectl apply -f k8s/deployment.yaml

kubectl apply -f k8s/service.yaml

---

## Verify

kubectl get deployments

kubectl get pods

kubectl get svc

---

## Port Forward Application

kubectl port-forward svc/task-manager-service 5000:80

Application URL:

http://localhost:5000

---

## Install Argo CD

kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

---

## Port Forward Argo CD

kubectl port-forward svc/argocd-server -n argocd 8080:443

Argo CD UI:

https://localhost:8080

---

## Get Admin Password

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | % { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }

---

## GitOps Workflow

1. Modify Kubernetes YAML
2. Commit changes
3. Push to GitHub
4. Argo CD detects changes
5. Kubernetes is updated automatically

---

## Technologies Used

- Python Flask
- Docker
- Kubernetes
- Kind
- Git
- GitHub
- Argo CD