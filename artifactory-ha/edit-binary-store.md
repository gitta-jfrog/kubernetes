

```yaml
artifactory:
    copyOnEveryStartup:
     - source: /artifactory_bootstrap/binarystore.xml
       target: etc/artifactory/
    persistence:
      maxCacheSize: 5135000000000
```
