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
kubecx


```bash
docker run -p 80:80 nginx
```
## ArgoCD

/charts folder installs Argo CD Helm chart 

/apps/templates/argo-cd.yaml makes sure that Argo CD manages itself (instead of using helm upgrade)

https://www.arthurkoziel.com/setting-up-argocd-with-helm/
### Install ArgCD Helm Chart

Run this to get started from scratch... 
```bash
helm install argo-cd charts/argo-cd/
```

```bash
helm template apps/ | kubectl apply -f -   
```

### Accessing ArgoCD Web UI / Dashboard

```bash
kubectl port-forward svc/argo-cd-argocd-server 8080:443
```

#### Get password for Login

Default Username is admin.

```bash
kubectl get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

```

## HELM

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

# Static website
```bash
 kubectl port-forward svc/static-website local-port:80
```

## Check connection is working
```bash
kubectl exec --stdin --tty static-website-576f89d7c6-blgn9 -n static-website -- /bin/bash
curl frost-server-frost-server-http.frost-server:80/FROST-Server/v1.1
```
# OTHER

## How To: Use local images within minikube
```bash
eval $(minikube docker-env)
```

```bash
docker build ... -t .
```

```bash
docker images # image should now be present
```

## Enable ingress controller (so DNS lookup works of services type ClusterIP)
```bash
minikube addons enable ingress
```