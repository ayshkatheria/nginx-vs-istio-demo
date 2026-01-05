# nginx-vs-istio-demo

```yaml
nginx-vs-istio-demo/
│
├── README.md
│
├── nginx-demo/
│   ├── app/
│   │   ├── app-v1.yaml
│   │   ├── app-v2.yaml
│   │   └── app1-service.yaml
│       ├── app2-service.yaml
│       └── ingress.yaml
│ 
│
├── istio-demo/
│   ├── app/
│   │   ├── app-v1.yaml
│   │   ├── app-v2.yaml
│   │   └── service.yaml
│   │
│   ├── traffic/
│   │   ├── destination-rule.yaml
│   │   ├── virtual-service.yaml
│   │
│   └── security/
│       └── mtls.yaml
│
└── demo-script/
    └── live-demo-steps.md
```
