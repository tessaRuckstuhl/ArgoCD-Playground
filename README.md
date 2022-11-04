# ArgoCD SC

```bash
docker run -p 80:80 nginx
```
# ArgoCD
## Install ArgCD Helm Chart

```bash
helm install argo-cd charts/argo-cd/
```

## Accessing ArgoCD Web UI / Dashboard

```bash
kubectl port-forward svc/argo-cd-argocd-server 8080:443
```

### Get password for Login

Default Username is admin.

```bash
kubectl get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

```

# HELM

```bash
helm template apps/ | kubectl apply -f -   
```

## Preview 
```bash
helm template apps/ | > preview.yaml   
```

## Get Template Locally
```bash
helm pull fraunhoferiosb/frost-server --untar
```


## POSTGIS

https://www.sumologic.com/blog/kubernetes-deploy-postgres/

```bash
kubectl exec -it postgres-687d5566f9-bxf6j -n postgisdb -- psql -U postgres
```

```bash 
kubectl port-forward svc/postgres 5432:5432 -n postgisdb
```

## FROSTSERVER

https://github.com/FraunhoferIOSB/FROST-Server/blob/v2.x/helm/frost-server/README.md