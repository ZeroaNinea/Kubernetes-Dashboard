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
127.0.0.1 dashboard.local
```

If you are using Linux type this command:

```bash
sudo nano /etc/hosts

```

Now add this line to the `hosts` file.

```plaintext
127.0.0.1 dashboard.local
```

Restart your PC to ensure the changes to the `hosts` file take effect. After restarting, it may take a few minutes for the Kubernetes Dashboard to become accessible.

Create an account, bind the Service Account to the Cluster Role, and get the Access Token:

```sh
kubectl create serviceaccount admin-user -n kubernetes-dashboard
kubectl create clusterrolebinding admin-user-binding --clusterrole=cluster-admin --serviceaccount=kubernetes-dashboard:admin-user
kubectl -n kubernetes-dashboard create token admin-user

```

Now you can access the dashboard using the [Dashboard](https://dashboard.local) URL in your browser or via `curl`:

```bash
curl -k https://dashboard.local

```

Alternatively, you can use `kubectl proxy`:

```sh
kubectl proxy

```

Then just visit this [link](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/).
