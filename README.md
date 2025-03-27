# Kubernetes Dashboard

To access this dashboard, use the following commands:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
kubectl apply -f dashboard-service.yaml
kubectl apply -f dashboard-ingress.yaml

```

Then edit the `hosts` file located at `C:\Windows\System32\drivers\etc\hosts` and add the following line:

```plaintext
127.0.0.1  dashboard.local
```

Create an account, bind the Service Account to the Cluster Role, get the Access Token:

```sh
kubectl create serviceaccount admin-user -n kubernetes-dashboard
kubectl create clusterrolebinding admin-user-binding --clusterrole=cluster-admin --serviceaccount=kubernetes-dashboard:admin-user
kubectl -n kubernetes-dashboard create token admin-user

```

Now you can access the dashboard using the [Dashboard](https://dashboard.local) URL in your browser or via `curl`:

```bash
curl -k https://dashboard.local

```

Alternatively you can use `kubectl proxy`:

```sh
kubectl proxy

```

Then just visit this [link](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/).
