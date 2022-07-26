

1. Install "AWS Load Balancer Controller"

https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/deploy/installation/

3. Install ingress-nginx Controller with custom configurations
```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
kubectl create ns artifactory
helm upgrade --install ingress-nginx --namespace artifactory ingress-nginx/ingress-nginx -f values-ingress-alb.yaml
```

3.Deploy Ingress Object for HTTPS Redirect
```
kubectl -n artifactory apply -f alb-ingress-nginx-controller.yaml    
```

4. Deploy Artifactory with custom configurations:
```
helm upgrade --install artifactory --namespace artifactory jfrog/artifactory -f values-artifactory-alb-ingress.yaml
```
