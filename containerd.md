


### use systemd as cgroup driver

```sh
sudo mkdir /etc/containerd
sudo sh -c "containerd config default > /etc/containerd/config.toml"
sudo cat /etc/containerd/config.toml | grep -i systemd
sudo sed -i "s/SystemdCgoup = false/SystemdCgroup = true/" /etc/containerd/config.toml
sudo systemctl restart containerd.service
```

# Use harbor as containerd mirror registry
<https://github.com/containerd/containerd/blob/main/docs/hosts.md#override_path-field>

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



### kubespray!
```yaml

containerd_registries_mirrors:
 - prefix: docker.io
   mirrors:
    - host: https://registry.site.io/v2/docker
      capabilities: ["pull", "resolve"]
      skip_verify: false
      override_path: true
 - prefix: registry.k8s.io
   mirrors:
    - host: https://registry.site.io/v2/k8s
      capabilities: ["pull", "resolve"]
      skip_verify: false
      override_path: true
 - prefix: ghcr.io
   mirrors:
    - host: https://registry.site.io/v2/ghcr
      capabilities: ["pull", "resolve"]
      skip_verify: false
      override_path: true
 - prefix: quay.io
   mirrors:
    - host: https://registry.site.io/v2/quay
      capabilities: ["pull", "resolve"]
      skip_verify: false
      override_path: true
 - prefix: gcr.io
   mirrors:
    - host: https://registry.site.io/v2/gcr
      capabilities: ["pull", "resolve"]
      skip_verify: false
      override_path: true
 - prefix: nvcr.io
   mirrors:
    - host: https://registry.site.io/v2/nvcr
      capabilities: ["pull", "resolve"]
      skip_verify: false
      override_path: true
 - prefix: mcr.microsoft.com
   mirrors:
    - host: https://registry.site.io/v2/mcr
      capabilities: ["pull", "resolve"]
      skip_verify: false
      override_path: true

```








