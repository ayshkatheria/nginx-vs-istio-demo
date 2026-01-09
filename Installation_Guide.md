```yaml
How to setup Istio on kubeadm hosted on EC2?

1. Create Security Group (Inbound Traffic)
  Open port:- 22 for SSH
              6443 for k8s API traffic
              179 for Calico uses BGP

2. Setup Kubeadm using below link on EC2 instances.
https://github.com/ayshkatheria/kubestarter/tree/main/Kubeadm_Installation_Scripts_and_Documentation

```
