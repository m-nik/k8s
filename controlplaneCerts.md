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

### apply for static pod
on every master node:
```
openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate

crictl ps | grep kube-apiserver
sudo mv /etc/kubernetes/manifests/kube-apiserver.yaml /tmp/
sleep 20
sudo mv /tmp/kube-apiserver.yaml /etc/kubernetes/manifests/kube-apiserver.yaml
crictl ps | grep kube-apiserver
```
And then:
```
systemctl restart kubelet.service
```
