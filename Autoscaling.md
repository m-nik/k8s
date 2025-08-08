### manually scale up and down
```
kubectl scale deployment flask-web-app --replicas 3
```

# Horizontal Pod Autoscaling (HPA)
```yml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  creationTimestamp: null
  name: nginx-deployment
spec:
  maxReplicas: 3
  metrics:
  - resource:
      name: cpu
      target:
        averageUtilization: 80
        type: Utilization
    type: Resource
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
status:
  currentMetrics: null
  desiredReplicas: 0
```
### watch hpa status
```sh
kubectl get hpa
kubectl get hpa --watch
```


# Vertical Pod Autoscaling (VPA)
<https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler>
```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: flask-app
  namespace: default
spec:
  resourcePolicy:
    containerPolicies:
    - containerName: '*'
      controlledResources:
      - cpu
      - memory
      maxAllowed:
        cpu: 1
        memory: 500Mi
      minAllowed:
        cpu: 100m
        memory: 100Mi
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: flask-app
  updatePolicy:
    evictionRequirements:
    - changeRequirement: TargetHigherThanRequests
      resources:
      - cpu
      - memory
    updateMode: Recreate
```
