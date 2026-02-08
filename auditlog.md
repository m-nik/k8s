
### kube-apiserver
```sh
mkdir -p /var/log/kubernetes
mkdir -p /etc/kubernetes/audit/
```
/etc/kubernetes/audit/audit-policy.yaml
```yaml
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
  - level: Metadata
```
/etc/kubernetes/manifests/kube-apiserver.yaml
```
    - --audit-log-path=/var/log/kubernetes/audit.log
    - --audit-policy-file=/etc/kubernetes/audit/audit-policy.yaml
    - --audit-log-maxage=5
    - --audit-log-maxbackup=2
    - --audit-log-maxsize=10
```
```
    volumeMounts:
    - mountPath: /etc/kubernetes/audit
      name: audit-policy-path
      readOnly: true
    - mountPath: /var/log/kubernetes/
      name: audit-log-path
```
```
  volumes:
  - hostPath:
      path: /etc/kubernetes/audit
      type: DirectoryOrCreate
    name: audit-policy-path
  - hostPath:
      path: /var/log/kubernetes/
      type: DirectoryOrCreate
    name: audit-log-path
```
