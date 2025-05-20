```sh
curl 127.0.0.1:10249/metrics
  # successful
curl 192.168.1.1:10249/metrics
  # Connection refused
sudo ss -tulnp | grep 10249
  # 127.0.0.1:10249
kubectl -n kube-system edit configmap kube-proxy
  # metricsBindAddress: 0.0.0.0:10249
kubectl -n kube-system rollout restart daemonset kube-proxy
kubectl get pod -n kube-system | grep kube-proxy
```
