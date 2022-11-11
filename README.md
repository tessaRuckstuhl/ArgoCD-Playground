# ArgoCD SC

Frost Server

- fraunhoferiosb/frost-server-http (web)
- fraunhoferiosb/frost-server-mqtt (mqtt)
- eclipse-mosquitto (mosquitto)
- postgis/postgis (database)

Other
- dpage/pgadmin4 (pgadmin)
- node-red
- grafana
- simulator
- geoserver 
- geoserver_db

## (Local) Setup ArgoCD apps-of-apps with Helm

```bash
# load images into minikube env...
minikube start 
eval $(minikube docker-env)
minikube image load static-website
minikube image load simulator-device
minikube image load angular-webapp

# enable ingress for minikube and check it is running - https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/


minikube addons enable ingress 
kubectl get pods -n ingress-nginx

# setup argo-cd with helm
helm install argo-cd charts/argo-cd/
helm template apps/ | kubectl apply -f -   

#check if everything is running correcly...
kubectl get pods -o wide -A
```

## ArgoCD

/charts folder installs Argo CD Helm chart 

/apps/templates/argo-cd.yaml makes sure that Argo CD manages itself (instead of using helm upgrade)

ref: https://www.arthurkoziel.com/setting-up-argocd-with-helm/

### Accessing ArgoCD Web UI / Dashboard

```bash
#get password, default username is admin
kubectl get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
#forward web ui
kubectl port-forward svc/argo-cd-argocd-server 8080:443
```
## HELM

### Preview 
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
kubectl port-forward svc/frost-server-frost-server-http 8081:80 -n frost-server 
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
kubectl exec --stdin --tty angular-webapp-76d559f54b-bhbhp -n angular-webapp -- /bin/bash
curl frost-server-frost-server-http.frost-server:80/FROST-Server/v1.1 -v
```

```bash
kubectl port-forward svc/angular-webapp 8082:80 -n angular-webapp
```