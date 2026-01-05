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
│   │   └── service.yaml
│   │
│   └── nginx/
│       ├── nginx-deployment.yaml
│       └── nginx.conf
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
