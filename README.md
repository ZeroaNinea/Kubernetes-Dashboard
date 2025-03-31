# Kubernetes Dashboard Deployment Guide

This repository provides instructions to deploy the Kubernetes Dashboard. Follow the steps below to set up and access the dashboard.

---

## Prerequisites

- A Kubernetes cluster (e.g., Minikube).
- `kubectl` CLI installed and configured.
- Basic knowledge of Kubernetes.

---

## Step 1: Enable Ingress (Minikube Only)

If you're using Minikube, enable the ingress addon:

```bash
minikube addons enable ingress
minikube stop
minikube start

```

---

## Step 2: Deploy Kubernetes Dashboard and Ingress Controller

Run the following commands to deploy the Kubernetes Dashboard, the ingress controller and `.yaml` files:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
kubectl apply -f dashboard-service.yaml
kubectl apply -f dashboard-ingress.yaml

```

---

## Step 3: Configure Hostname Resolution

### For Windows:
1. Edit the `hosts` file located at:
   ```
   C:\Windows\System32\drivers\etc\hosts
   ```
2. Add the following line:
   ```plaintext
   127.0.0.1 dashboard.local
   ```

### For Linux:
1. Open the `hosts` file:
   ```bash
   sudo nano /etc/hosts
   ```
2. Add the following line:
   ```plaintext
   127.0.0.1 dashboard.local
   ```

Restart your PC to apply the changes.

---

## Step 4: Create Service Account and Access Token

Run the following commands to create an admin service account, bind it to the cluster role, and retrieve the access token:

```bash
kubectl create serviceaccount admin-user -n kubernetes-dashboard
kubectl create clusterrolebinding admin-user-binding --clusterrole=cluster-admin --serviceaccount=kubernetes-dashboard:admin-user
kubectl -n kubernetes-dashboard create token admin-user

```

---

## Step 5: Access the Dashboard

### Option 1: Using a Browser
Visit the following URL in your browser:
- [https://dashboard.local](https://dashboard.local)

### Option 2: Using `curl`
Run the following command:
```bash
curl -k https://dashboard.local
```

### Option 3: Using `kubectl proxy`
Start the proxy:
```bash
kubectl proxy
```
Then visit:
- [http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/)

---

## Notes

- It may take a few minutes for the dashboard to become accessible after deployment.
- Ensure your cluster is running and properly configured before starting.

For more information, visit the [Kubernetes Dashboard documentation](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).
