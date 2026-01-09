1. Ensure multiple versions exist

> kubectl get pods -l app=reviews

2. Define subsets (DestinationRule) 

Create destination-rule-reviews.yaml

3. Create Canary traffic split (VirtualService)

create virtual-service-reviews-canary.yaml

>kubectl apply -f virtual-service-reviews-canary.yaml

What this does

90% traffic → v1 (stable)

10% traffic → v2 (canary)

4. To Test hitt url in browser
http://<INGRESS-IP>:<NODEPORT>/productpage


