

1. Install Nginx-ingrss Controller

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

5. Redeploy Nginx-ingress controller:
```bash
helm upgrade --install nginx-ingress --namespace nginx-ingress center/kubernetes-ingress-nginx/ingress-nginx -f values-ingress.yaml
```
