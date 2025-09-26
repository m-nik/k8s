
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
