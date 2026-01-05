```yaml
Browser
  |
NGINX Ingress Controller
  |
-------------------------
|                       |
/app1 → app1 service   /app2 → app2 service

Note:
NGINX is NOT used to create an ALB.
NGINX is only used to ROUTE traffic AFTER it reaches the cluster.

```

```yaml

kubectl apply -f app-v1.yaml
kubectl apply -f app-v2.yaml

kubectl apply -f app1-svc.yaml
kubectl apply -f app2-svc.yaml


Install NGINX Ingress Controller

> kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml

verify:
> kubectl get pods -n ingress-nginx

kubectl apply -f ingress.yaml


Test internally (always works)
kubectl exec -it deploy/app-v1 -- curl http://app1
kubectl exec -it deploy/app-v2 -- curl http://app2

Port-forward Ingress Controller (kodekloud)
kubectl port-forward -n ingress-nginx svc/ingress-nginx-controller 9000:80 --address 0.0.0.0

Hit url in browser:
http://9000-port-<your-id>.labs.kodekloud.com/app1
http://9000-port-<your-id>.labs.kodekloud.com/app2

```

