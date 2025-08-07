# Priority Classes
```sh
kubectl get pc
kubectl get priorityclasses
```

### ranges
Over 2,000,000,000 ==> system-cluster-critical
Between 1,000,000,000 and -2,000,000,000 == > user defined

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

### priorityClassName in pod definition
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: low-prio-pod
spec:
  containers:
  - name: nginx
    image: nginx
  priorityClassName: low-priority
```


### get priorityClassName in pod list
```sh
kubectl get pods -o custom-columns="NAME:.metadata.name,PRIORITY:.spec.priorityClassName"
```

<https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption>
