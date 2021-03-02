## Artifactory (outside cluster)

1. Define shared.node.ip in Artifactory system.yaml (IP address/DNS must be accessible from the pod running inside the K8S cluster):

```yaml
shared:
  node:
    ip: <ARTIFACTORY_EXTERNAL_IP>
```

## Xray (inside K8S cluster)

1. Deploy Xray Helm Chart with the following values.yaml:

```yaml
server: 
  service:
    type: "LoadBalancer"
    annotations:
      service.alpha.kubernetes.io/tolerate-unready-endpoints: "true"
```

2. Extract the External IP of the service we set the IP at the systemYaml section and deploy the chart again.

```yaml
server: 
  service:
    type: "LoadBalancer"
    annotations:
      service.alpha.kubernetes.io/tolerate-unready-endpoints: "true"
xray:
  systemYaml: |
    configVersion: 1
    shared:
      node:
        ip: <XRAY_EXTERNAL_IP>
      logging:
        consoleLog:
          enabled: {{ .Values.xray.consoleLog }}
      jfrogUrl: "{{ tpl (required "\n\nxray.jfrogUrl or global.jfrogUrl is required! This allows to connect to Artifactory.\nYou can copy the JFrog URL from Admin > Security > Settings" (include "xray.jfrogUrl" .)) . }}"
      database:
      {{- if .Values.postgresql.enabled }}
        type: "postgresql"
        driver: "org.postgresql.Driver"
        username: "{{ .Values.postgresql.postgresqlUsername }}"
        url: "postgres://{{ .Release.Name }}-postgresql:{{ .Values.postgresql.service.port }}/{{ .Values.postgresql.postgresqlDatabase }}?sslmode=disable"
      {{- else }}
        type: {{ .Values.database.type }}
        driver: {{ .Values.database.driver }}
      {{- end }}
      {{- if and (not .Values.rabbitmq.enabled) (not .Values.common.rabbitmq.connectionConfigFromEnvironment) }}
      rabbitMq:
        erlangCookie:
          value: "{{ .Values.rabbitmq.external.erlangCookie }}"
      {{- if not .Values.rabbitmq.external.secrets }}
        url: "{{ tpl .Values.rabbitmq.external.url . }}"
        username: "{{ .Values.rabbitmq.external.username }}"
        password: "{{ .Values.rabbitmq.external.password }}"
      {{- end }}
      {{- end }}
      {{- if .Values.xray.mongoUrl }}
      mongo:
        url: "{{ .Values.xray.mongoUrl }}"
        username: "{{ .Values.xray.mongoUsername }}"
        password: "{{ .Values.xray.mongoPassword }}"
      {{- end }}
    server:
      mailServer: "{{ .Values.server.mailServer }}"
      indexAllBuilds: "{{ .Values.server.indexAllBuilds }}"
```
