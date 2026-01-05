```yaml
NGINX routes requests.
Istio controls traffic behavior.
```

```yaml
kubectl apply -f app-v1.yaml
kubectl apply -f app-v2.yaml

kubectl apply -f app-service.yaml

kubectl apply -f destination-rule.yaml

kubectl apply -f virtual-service.yaml

Test Istio Traffic
kubectl exec -it deploy/app-v1 -- curl http://app

```

```yaml
🔥 ONE thing Istio does that NGINX CANNOT do cleanly
Route only beta users to v2

http:
- match:
  - headers:
      x-user:
        exact: beta
  route:
  - destination:
      host: app
      subset: v2

```
👉 No app changes
👉 No proxy reload
👉 No central bottleneck

```yaml
Generate traffic
for i in {1..100}; do
  kubectl exec -it deploy/app-v1 -- curl -s http://app > /dev/null
done

```
