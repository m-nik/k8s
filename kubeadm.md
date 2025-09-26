
## install kubeadm
```sh
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
```


## Initialize cluster
```sh
sudo kubeadm init --dry-run
sudo kubeadm init --apiserver-advertise-address 192.168.11.201 --pod-network-cidr 10.244.0.0/16 --upload-certs
```

use `--image-repository` to speedup pulling k8s images in a local network

## Use a config file and override defaults
```sh
kubeadm config print init-defaults > kubeadm-config.yaml
kubeadm init --config kubeadm-config.yaml
```


## list and pull images
```sh
kubeadm config images list
kubeadm config images pull
```



## Issue: CoreDNS image and path-based container image registry

```sh
kubeadm config images list
  registry.k8s.io/kube-apiserver:v1.33.5
  registry.k8s.io/kube-controller-manager:v1.33.5
  registry.k8s.io/kube-scheduler:v1.33.5
  registry.k8s.io/kube-proxy:v1.33.5
  registry.k8s.io/coredns/coredns:v1.12.0
  registry.k8s.io/pause:3.10
  registry.k8s.io/etcd:3.5.21-0
```
When using a path-based container image registry (e.g., Harbor) that adds an extra path, like:
```
registry.company.io/k8s
```
kubeadm may generate an incorrect CoreDNS image path:

Expected: `registry.company.io/k8s/coredns/coredns:v1.12.0`

Generated: `registry.company.io/k8s/coredns:v1.12.0`

This causes image pull failures. This is a [known issue in kubeadm](https://github.com/kubernetes/kubeadm/issues/2525?utm_source=chatgpt.com)


#### Solution

Use a minimal ClusterConfiguration YAML that overrides the CoreDNS image:
```yaml
apiVersion: kubeadm.k8s.io/v1beta3
kind: ClusterConfiguration
kubernetesVersion: "v1.33.5"
controlPlaneEndpoint: "10.0.2.15:6443"
imageRepository: registry.company.io/k8s
networking:
  podSubnet: "10.244.0.0/16"
dns:
  type: CoreDNS
  imageRepository: registry.company.io/k8s/coredns
  imageTag: v1.12.0
```
```sh
sudo kubeadm init --config kubeadm-minimal.yaml --upload-certs
```
