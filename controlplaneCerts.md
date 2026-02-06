# kubeadm
### check-expiration
on controlplane nodes:
```
sudo kubeadm certs check-expiration
```

### renew
```
sudo kubeadm certs renew all
sudo systemctl restart kubelet
```
