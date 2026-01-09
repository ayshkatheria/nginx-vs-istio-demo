```yaml
How to setup Istio on kubeadm hosted on EC2?

1. Create Security Group (Inbound Traffic)
  Open port:- 22 for SSH
              6443 for k8s API traffic
              179 for Calico uses BGP

2. Setup Kubeadm using below link on EC2 instances.
   https://github.com/ayshkatheria/kubestarter/tree/main/Kubeadm_Installation_Scripts_and_Documentation

3. Download and install Istion on k8s cluster 

> curl -L https://istio.io/downloadIstio | sh -

> cd istio-1.28.2

> export PATH=$PWD/bin:$PATH

4. Now Install configure profiles.

> istioctl install --set profile=default

It will install below :-

✔ Istio core installed ⛵️
✔ Istiod installed 🧠
✔ Ingress gateways installed 🛬
✔ Installation complete

Istio links for download & installation 
https://istio.io/latest/docs/setup/additional-setup/config-profiles/
https://istio.io/latest/docs/setup/additional-setup/download-istio-release/

```
