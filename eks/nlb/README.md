


## Setup definitions

1. Installation of Artifactory-HA on EKS Cluster 
2. All incoming configration goes through AWS Network LoadBalancer(NLB).  https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html
3. Artifactory TLS Enabled https://www.jfrog.com/confluence/display/JFROG/Managing+TLS+Certificates#ManagingTLSCertificates-EnablingTLSintheJFrogPlatform
4. Nginx configurations:
*Option A: Using Internal Nginx deployment as part of Artifactory-HA helm chart.
*Option B: Using Nginx-Ingress controller (https://kubernetes.github.io/ingress-nginx/)

## Setup challenges

1. Artifactory with TLS Enabled - By default, TLS in the JFrog Platform is disabled. When TLS is enabled, all communications to the JFrog Platform are required to use TLS including service-to-service communication within the platform. 
* Communications to the JFrog Router at port 8082 - HTTPS only.
* Communications to Artifactory Tomcat at port 8081 (/artifactory) - HTTP only.


2. Using AWS NLB with SSL termination - AWS NLB support the ability to make use of TLS connections that terminate at a Network Load Balancer with ACM certificate.
https://aws.amazon.com/blogs/aws/new-tls-termination-for-network-load-balancers/
https://github.com/kubernetes/kubernetes/issues/73297

3. Verify HTTPS connection from the client to Artifactory, even that SSL termination in the NLB. Requiered for "docker push" command.


## Final setup

1. Artifactory with TLS enabled.
2. NLB with specific certificate
3. Nginx special configuration:
```yaml
proxy_set_header    X-Forwarded-Proto https
```
