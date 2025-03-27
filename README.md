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

Now you can access the dashboard using the [Dashboard](https://dashboard.local) URL in your browser or via `curl`:

```bash
curl -k https://dashboard.local

```
