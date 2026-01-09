```yaml

1. Confirm sidecar injection

>kubectl get ns default --show-labels

expected output:- istio-injection=enabled

If not:

>kubectl label namespace default istio-injection=enabled
>kubectl rollout restart deploy -n default


Step 2 — Enable STRICT mTLS (server-side)
Create peer-authentication-strict.yaml

>kubectl apply -f peer-authentication-strict.yaml
>kubectl get peerauthentication -n default

Step 3 — Enforce mTLS on clients (client-side)
destination-rule-istio-mutual.yaml

> kubectl apply -f destination-rule-istio-mutual.yaml

Step 4 — Test mTLS traffic (should WORK)

> kubectl exec -it \
  "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" \
  -c ratings -- curl -s productpage:9080/productpage | grep "<title>"

expected o/p:

<title>Simple Bookstore App</title>


Step 5 — Verify at Envoy level (optional but strong proof)

>kubectl exec -it \
  "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" \
  -c istio-proxy -- \
  curl -s localhost:15000/config_dump | grep -i require_client_certificate

  expected o/p : "require_client_certificate": true

  Step 6 — Rollback to PERMISSIVE (if needed)

  >kubectl delete peerauthentication default -n default  
  >kubectl delete destinationrule default-mtls -n default

```

```yaml 

Pod A  ───────▶  Pod B
(client)          (server)

Client = the pod making the request

Server = the pod receiving the request

Both have Envoy sidecars

Envoy handles mTLS, not your application code


Client Pod
  └── Envoy (has cert)
        │
        │  mTLS (cert + encryption)
        ▼
Server Envoy
  └── STRICT PeerAuthentication
        │
        ▼
Service


```

















