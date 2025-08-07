# Priority Classes
```sh
kubectl get pc
kubectl get priorityclasses
```

### define
```yaml
apiVersion: scheduling.k8s.io/v1
description: low-priority PriorityClass
kind: PriorityClass
metadata:
  name: low-priority
value: 1000
```
