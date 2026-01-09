```yaml

--------------------mTLS in PERMISSIVE (passive) mode-----------------------------------

check: Is any strict mTLS policy applied?

>kubectl get peerauthentication -A

o/p :- No resources found (No STRICT policy, Namespace is running in PERMISSIVE by default)

1. Verify traffic works without certificates

kubectl exec -it \
  "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" \
  -c ratings -- curl -s productpage:9080/productpage

2. Check Envoy confirms PERMISSIVE mode

kubectl exec -n default \
  "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" \
  -c istio-proxy -- curl -s localhost:15000/config_dump \
  | grep -i tls


```yaml
To access the Bookinfo app from outside the cluster when using Istio, you expose it through the Istio Ingress Gateway.

```

1. Verify Istio Ingress Gateway is running

>kubectl get pods -n istio-system -l app=istio-ingressgateway

2. Create Gateway + VirtualService (Bookinfo)

>kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml

Verify : 
> kubectl get gateway
> kubectl get virtualservice

3. Set GATEWAY_URL
> export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT

4. Find how to reach the Ingress Gateway EC2

Option A — NodePort (most common with kubeadm)
> kubectl get svc -n istio-system istio-ingressgateway

👉 Use the NodePort mapped to port 80 (e.g., 30yyy).

http://<EC2_PUBLIC_IP>:<NODEPORT>/productpage

Note: Make sure your EC2 Security Group allows that NodePort range (30000–32767).

Option B — Port-forward (quick test, no SG changes)
kubectl port-forward -n istio-system svc/istio-ingressgateway 8080:80
http://localhost:8080/productpage
```

```
