# nexus on docker
```yaml
services:
  nexus:
    image: sonatype/nexus3
    restart: always
    volumes:
      - "./data:/sonatype-work"
    ports:
      - "8081:8081"
      - "8082:8082"
      - "8083:8083"
      - "8084:8084"
```
# K8s cluster importants repos
- https://quay.io
- https://registry.k8s.io
- https://registry-1.docker.io
  
Map each one on a port

# Nginx sample config
```nginx
server{
	server_name k8s.site.info;
    location / {
      proxy_pass http://192.168.1.1:8083;
      proxy_buffering off;
      proxy_request_buffering off;
      proxy_send_timeout 90;
      proxy_read_timeout 90;
      client_max_body_size 500M;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
      proxy_set_header X-Forwarded-Host $host;
    }
    listen 80;
}
```
# Upload helm charts to a hosted helm repo
```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
helm pull bitnami/redis --version 20.6.1
curl -u user:password https://nexus.site.info/repository/helm-charts/ --upload-file redis-20.6.1.tgz 
```
# Add each one to containerd registries
```toml
server = "https://quay.io"
[host."https://quay.site.info"]
  capabilities = ["pull","resolve"]
  skip_verify = false
  override_path = false
```
