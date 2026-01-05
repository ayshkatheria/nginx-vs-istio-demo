```yaml
✅ STEP 1: Install Istio (recommended way)
1️⃣ Download Istio
curl -L https://istio.io/downloadIstio | sh -
cd istio-*

2️⃣ Install istioctl
sudo mv bin/istioctl /usr/local/bin/
istioctl version

✅ STEP 2: Install Istio control plane

For kubeadm + EC2, use demo profile (best for learning):

istioctl install --set profile=demo -y
Verify:
kubectl get pods -n istio-system

You should see:
istiod
istio-ingressgateway

✅ STEP 3: Enable sidecar injection for your app namespace

Your apps are in default namespace.

kubectl label namespace default istio-injection=enabled


Restart app pods (IMPORTANT):

kubectl rollout restart deploy/app-v1
kubectl rollout restart deploy/app-v2

Verify sidecars:

kubectl get pods


You should see:

2/2   Running
(nginx + envoy)

✅ STEP 4: Expose apps via Istio Gateway
1️⃣ Create istio-gateway.yaml
2️⃣ Create VirtualService
2️⃣ Create DestinationRule & VirtualService

✅ STEP 5: Access Istio Ingress (VERY IMPORTANT)

Check Istio ingress service:

kubectl get svc -n istio-system istio-ingressgateway

✅ STEP 7 (OPTIONAL BUT AWESOME): Kiali
kubectl apply -f samples/addons/kiali.yaml
kubectl apply -f samples/addons/prometheus.yaml

```

```yaml
✅ STEP 1: Install Kiali + Prometheus (REQUIRED)

Kiali needs Prometheus to show traffic.

From your Istio directory (istio-1.28.2):

kubectl apply -f samples/addons/prometheus.yaml
kubectl apply -f samples/addons/kiali.yaml

Verify:

kubectl get pods -n istio-system

```

```yaml
✅ STEP 2: SSH port-forward from your laptop

From your local laptop, run:
ssh -i <key.pem> -L 20001:localhost:20001 ubuntu@<EC2_PUBLIC_IP>

use master node config

Now open browser on your laptop:

http://localhost:20001/kiali
```

```yaml
🧪 If Kiali page is blank / no graph

Do this:

Select Namespace → default

Click Graph

Generate traffic:

while true; do
  curl http://<WORKER_ELASTIC_IP>:30267/app1 > /dev/null
  sleep 1
done
```











