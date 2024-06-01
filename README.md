# nginx-mqtt-njs
Repo to configure NGINX Plus as ingress controller for MQTT traffic, using NGINX JavaScript (NJS) to route new inbound connections to pre-determined pods by hostname.

#### Deploy NGINX

Replace `jwt-token-data` with base64-encoded JWT token for pulling NGINX Plus Ingress Controller image.


```bash
kubectl apply -f common/ns-and-sa.yaml
kubectl create secret docker-registry regcred --docker-server=private-registry.nginx.com --docker-username=jwt-token-data --docker-password=none -n nginx-ingress
```

```bash

kubectl apply -f rbac/rbac.yaml
kubectl apply -f common/default-server-secret.yaml
kubectl apply -f common/nginx-config.yaml
kubectl apply -f common/ingress-class.yaml

kubectl apply -f https://raw.githubusercontent.com/nginxinc/kubernetes-ingress/v3.5.2/deploy/crds.yaml

kubectl apply -f deployment/nginx-plus-ingress.yaml

kubectl create -f service/clusterip.yaml

```