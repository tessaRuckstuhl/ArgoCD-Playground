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

# HELM

```bash
helm template apps/ | kubectl apply -f -   
```


```bash
helm template apps/ | > preview.yaml   
```


## POSTGIS

https://www.sumologic.com/blog/kubernetes-deploy-postgres/

```bash
kubectl exec -it postgres-687d5566f9-bxf6j -n postgisdb -- psql -U postgres
```

```bash 
kubectl port-forward svc/postgres 5432:5432 -n postgisdb
```

