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

### preemptionPolicy
```yaml
apiVersion: scheduling.k8s.io/v1
description: high-priority PriorityClass
kind: PriorityClass
metadata:
  name: high-priority
preemptionPolicy: PreemptLowerPriority
value: 1000000
```

