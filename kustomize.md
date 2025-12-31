```
k8s/
├── base/
│   ├── backend/
│   └── frontend/
│
├── components/
│   ├── mongo/
│   │   ├── statefulset.yaml
│   │   ├── service.yaml
│   │   └── kustomization.yaml
│   └── rabbitmq/
│       ├── statefulset.yaml
│       ├── service.yaml
│       └── kustomization.yaml
│
└── overlays/
    └── stage/
        ├── backend/
        ├── frontend/
        └── kustomization.yaml
```


### Garbage collection
```
kubectl apply -k stage --prune -l app-config=secret
```
