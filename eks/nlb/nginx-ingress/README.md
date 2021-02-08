

1. Install Nginx-ingrss Controller
```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
kubectl create ns nginx-ingress
helm upgrade --install nginx-ingress --namespace nginx-ingress ingress-nginx/ingress-nginx -f values-ingress.yaml
```

2. Export nginx.tmpl file:

To copy the nginx template file from the ingress controller pod to your local machine, you can first grab the name of the pod with kubectl get pods then run:

```bash
kubectl exec [POD_NAME] -it -- cat /etc/nginx/template/nginx.tmpl > nginx.tmpl
```

3. Edit nginx.tmpl

Replace:
```yaml
{{ $proxySetHeader }} X-Forwarded-Proto      $pass_access_scheme;

```

With:
```yaml
{{ $proxySetHeader }} X-Forwarded-Proto      https;

```

4. 
```bash
kubectl create configmap custom-nginx-template --from-file nginx.tmpl  -n nginx-ingress 
```
5. Uncomment from values-ingress.yaml:
```yaml
controller:
  customTemplate:
    configMapName: "nginx-https-gitta"
    configMapKey: "nginx.tmpl"
```

5. Redeploy Nginx-ingress controller:
```bash
helm upgrade --install nginx-ingress --namespace nginx-ingress center/kubernetes-ingress-nginx/ingress-nginx -f values-ingress.yaml
```
