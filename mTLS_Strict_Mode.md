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
