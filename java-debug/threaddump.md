```
echo -e "PID=\$(pgrep java);
for ((count=1; count <= 10000; count++));
do /opt/jfrog/artifactory/app/third-party/java/bin/jstack -l \$PID  > /opt/jfrog/artifactory/var/log/artifactory-\$(date +%Y%m%d%H%M%S)-td.log
echo \$(date) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Artifactory \$(curl -s -o /dev/null -w '%{http_code}' localhost:8081/artifactory/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Router \$(curl -s -o /dev/null -w '%{http_code}' localhost:8082/router/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Access \$(curl -s -o /dev/null -w '%{http_code}' localhost:8040/access/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Metadata \$(curl -s -o /dev/null -w '%{http_code}' localhost:8086/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Frontend \$(curl -s -o /dev/null -w '%{http_code}' localhost:8070/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Event \$(curl -s -o /dev/null -w '%{http_code}' localhost:8061/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Observability \$(curl -s -o /dev/null -w '%{http_code}' localhost:8036/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo Integration \$(curl -s -o /dev/null -w '%{http_code}' localhost:8071/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo JFconnect \$(curl -s -o /dev/null -w '%{http_code}' localhost:8030/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo MissionControl \$(curl -s -o /dev/null -w '%{http_code}' localhost:8091/mc/api/v1/system/readiness) >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log
echo '' >> /opt/jfrog/artifactory/var/log/artifactory-monitoring.log

sleep 5s;
done;" > debug.sh

```
```
chmod +x debug.sh

```
./debug.sh
