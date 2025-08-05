## push a chart to harbor
```
helm registry login registry.site.info/helm-charts --username USER
helm push pulsar-4.1.0.tgz oci://registry.site.info/helm-charts
```

## push a chart to nexus
```
curl -u user:pass https://registry.site.info/repository/helm-charts/ --upload-file prometheus-pushgateway-3.4.0.tgz
```

