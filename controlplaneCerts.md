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

### debug
```
openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate
```

### apply for static pods
```
crictl ps | grep kube-apiserver
sudo mv /etc/kubernetes/manifests/kube-apiserver.yaml /tmp/
sleep 20
sudo mv /tmp/kube-apiserver.yaml /etc/kubernetes/manifests/kube-apiserver.yaml
crictl ps | grep kube-apiserver
```
