# ArgoCD SC

```bash
docker run -p 80:80 nginx
```

## Install Argo CD Helm Chart

```bash
helm install argo-cd charts/argo-cd/
```

## Accessing the Web UI

```bash
kubectl port-forward svc/argo-cd-argocd-server 8080:443
```

## Get password

Default Username is admin.

```bash
kubectl get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

```