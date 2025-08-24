# Use harbor as containerd mirror registry
/etc/containerd/certs.d/docker.io/hosts.toml
```toml
server = "https://docker.io"
[host."https://registry.site.io/v2/docker"]
  capabilities = ["pull","resolve"]
  skip_verify = false
  override_path = true
```









