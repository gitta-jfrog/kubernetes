

Install Artifactory v6.x

```bash
helm upgrade --install art-6 --namespace art-6 --version=1.4.0 center/jfrog/artifactory-ha \
--set artifactory.masterKey="c601841ee4a874161d9fc596a6a1974c" \
--set artifactory.node.replicaCount=1 \
--set artifactory.persistence.size=50Gi \
--set postgresql.postgresqlUsername="artifactory" \
--set postgresql.postgresqlPassword="1WcseEOS4s" \
--set postgresql.persistence.size=50Gi \
--set databaseUpgradeReady=true \
--set unifiedUpgradeAllowed=true \
--set postgresql.image.tag="9.6.18-debian-10-r7" --set artifactory.license.secret=artifactory-cluster-license,artifactory.license.dataKey=art.lic
```
Delete sts
```bash
kubectl delete statefulsets <OLD_RELEASE_NAME>-postgresql
```

Upgrade Artifactory v6.x to v7.x
```bash
helm upgrade --install art-6 --namespace art-6 --version=4.5.2 center/jfrog/artifactory-ha \
--set artifactory.masterKey="c601841ee4a874161d9fc596a6a1974c" \
--set artifactory.node.replicaCount=1 \
--set artifactory.persistence.size=50Gi \
--set postgresql.postgresqlUsername="artifactory" \
--set postgresql.postgresqlPassword="1WcseEOS4s" \
--set postgresql.persistence.size=50Gi \
--set databaseUpgradeReady=true \
--set unifiedUpgradeAllowed=true \
--set artifactory.migration.enabled=true --set artifactory.migration.timeoutSeconds=3600 \
--set postgresql.image.tag="9.6.18-debian-10-r7" --set artifactory.license.secret=artifactory-cluster-license,artifactory.license.dataKey=art.lic
```


https://github.com/jfrog/charts/tree/master/stable/artifactory-ha#special-upgrade-notes
https://github.com/jfrog/charts/tree/master/stable/artifactory-ha#special-upgrade-notes-1

