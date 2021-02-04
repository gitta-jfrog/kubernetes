

```yaml
artifactory:
  persistence:
    maxCacheSize: 123000000000
  copyOnEveryStartup:
    - source: /artifactory_bootstrap/binarystore.xml
      target: etc/artifactory/
```
