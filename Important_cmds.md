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

```
