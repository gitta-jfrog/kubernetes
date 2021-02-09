


## Setup definitions

1. Installation of Artifactory-HA on EKS Cluster 
2. All incoming configration goes through AWS Network LoadBalancer(NLB).  https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html
3. Artifactory TLS Enabled https://www.jfrog.com/confluence/display/JFROG/Managing+TLS+Certificates#ManagingTLSCertificates-EnablingTLSintheJFrogPlatform
4. Nginx configurations:

  4a. Option A: Using Internal Nginx deployment as part of Artifactory-HA helm chart 
  4b. Option B: Using Nginx-Ingress controller (https://kubernetes.github.io/ingress-nginx/)
