Step 1 — Install Kiali (recommended way)

kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.28/samples/addons/kiali.yaml

This also installs:

Prometheus (required by Kiali)

Verify:

kubectl get pods -n istio-system | grep kiali

Important : Open port >> 20001

Step 2- ./istioctl dashboard kiali
