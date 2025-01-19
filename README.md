# 2048 Game Deployment on Kubernetes using KIND

This repository contains the configuration and files to deploy the classic 2048 game on local Kubernetes cluster using KIND.

The application is deployed as a NodePort service, allowing user to access the game via web browser.

## Prerequisites

Ensure you have the following tools installed:

- Docker Desktop (with Kubernetes enabled)
- KIND (Kubernetes IN Docker)
- kubectl (Kubernetes CLI)
- Git

## Setup and Run Instructions

Follow these steps to deploy and run the 2048 game on Kubernetes:

### 1. Create KIND Cluster
```bash
kind create cluster --config kind-cluster-config.yaml --name 2048-cluster
```
![image](https://github.com/user-attachments/assets/0373c8ce-35c5-45d9-815a-f1e1e26a12eb)

### Check nodes

![image](https://github.com/user-attachments/assets/90f098fb-78c6-44f5-87de-4c1e107abe14)


### 2. Build and Load Docker Image
```bash
docker build -t 2048-game:latest .
kind load docker-image 2048-game:latest --name 2048-cluster
```
![image](https://github.com/user-attachments/assets/383899ac-6810-46e7-aca5-a752e244e3ce)

![image](https://github.com/user-attachments/assets/d7c184b6-e352-4f1c-ae7f-9cc8f1eacf22)


### 3. Deploy to Kubernetes
```bash
kubectl apply -f manifests/
```
![image](https://github.com/user-attachments/assets/55e6695a-341f-4d1b-b373-17bfa8674e0e)

![image](https://github.com/user-attachments/assets/96539879-c38d-4245-8449-023e23c182cf)


### 4. Access the Game
1. Port forward the service:
```bash
kubectl port-forward svc/game2048-service 8080:80
```
![image](https://github.com/user-attachments/assets/c2c643a9-81d8-4eea-a384-b49e5cdf2d52)

2. Open a web browser and visit:
```bash
http://localhost:8080
```
![image](https://github.com/user-attachments/assets/53b7c5e2-ccd4-44a1-92a4-61010a16c724)





