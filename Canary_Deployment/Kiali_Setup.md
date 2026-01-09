```yaml

Step 1 — Install Kiali (recommended way)

kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.28/samples/addons/kiali.yaml

This also installs:
Prometheus (required by Kiali)

Verify:
kubectl get pods -n istio-system | grep kiali

Important : Open port >> 20001

Step-2 Make sure prometheus is up and running

kubectl get pods -n istio-system | grep prometheus

Install Prometheus (official Istio addon)

> kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.28/samples/addons/prometheus.yaml

Verify : Verify Prometheus is running
kubectl get pods -n istio-system | grep prometheus
kubectl get svc  -n istio-system | grep prometheus

Step- 3 Open a new terminal and start kiali 

> ssh -i <your-key.pem> \
  -L 20001:localhost:20001 \
  ubuntu@<EC2_PUBLIC_IP>


Step 4 - ./istioctl dashboard kiali

Step 5 - http://localhost:20001/kiali
```
