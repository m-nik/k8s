## push a chart to harbor
```
helm registry login registry.site.info/helm-charts --username USER
helm push pulsar-4.1.0.tgz oci://registry.site.info/helm-charts
```

