# ArgoCD SC

Frost Server

- fraunhoferiosb/frost-server-http (web)
- fraunhoferiosb/frost-server-mqtt (mqtt)
- eclipse-mosquitto (mosquitto)
- postgis/postgis (database)

- dpage/pgadmin4 (pgadmin)
- node-red
- grafana
- simulator
- geoserver 
- geoserver_db



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

# Nginx

# POSTGIS

https://www.sumologic.com/blog/kubernetes-deploy-postgres/

```bash
kubectl exec -it postgres-687d5566f9-bxf6j -n postgisdb -- psql -U postgres
```

```bash 
kubectl port-forward svc/postgres 5432:5432 -n postgisdb
```

# FROSTSERVER

https://github.com/FraunhoferIOSB/FROST-Server/blob/v2.x/helm/frost-server/README.md

## Forward
```bash
kubectl port-forward svc/frost-server-frost-server-http 8081:80 -n frostserver 
```

```bash
http://localhost:8081/FROST-Server/v1.1
```