```bash
helm repo add jfrog https://charts.jfrog.io
helm repo update
helm upgrade --install jfrog-platform --namespace jfrog-platform jfrog/jfrog-platform -f values-external-postgres.yaml -f values-platform-medium.yaml
```
