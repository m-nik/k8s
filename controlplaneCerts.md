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
crictl ps | grep kube-
sudo mv /etc/kubernetes/manifests/kube-apiserver.yaml /tmp/
sudo mv /etc/kubernetes/manifests/kube-controller-manager.yaml /tmp/
sudo mv /etc/kubernetes/manifests/kube-scheduler.yaml /tmp/
sleep 20
sudo mv /tmp/kube-apiserver.yaml /etc/kubernetes/manifests/kube-apiserver.yaml
sudo mv /tmp/kube-controller-manager.yaml /etc/kubernetes/manifests/kube-controller-manager.yaml
sudo mv /tmp/kube-scheduler.yaml /etc/kubernetes/manifests/kube-scheduler.yaml
```
And then:
```
systemctl restart kubelet.service
```
### update kube-config
```
cp /etc/kubernetes/admin.conf .kube/config
```
