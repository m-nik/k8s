# Use harbor as containerd mirror registry
/etc/containerd/certs.d/docker.io/hosts.toml
```toml
server = "https://docker.io"
[host."https://registry.site.io/v2/docker"]
  capabilities = ["pull","resolve"]
  skip_verify = false
  override_path = true
```
/etc/containerd/certs.d/registry.k8s.io/hosts.toml
```toml
server = "https://registry.k8s.io"
[host."https://registry.site.io/v2/k8s"]
  capabilities = ["pull","resolve"]
  skip_verify = false
  override_path = true
```





