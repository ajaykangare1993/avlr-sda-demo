# avlr-sda-demo
<img width="625" alt="Screenshot 2024-05-13 at 2 27 27 AM" src="https://github.com/ajaykangare1993/avlr-sda-demo/assets/169615774/d09fb9c3-5cec-41cb-97e9-23878eb85012">

To deploy bove mentioned application, run following commands:

1. Deploy Ingress Nginx Controller

   kubectl create ns ingress-nginx
   helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
   helm repo update

   helm install ingress-nginx ingress-nginx/ingress-nginx \
       --namespace ingress-nginx \
       --set controller.replicaCount=1 \
       --set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
       --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
       --set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
       --set defaultBackend.image.digest="" 
    
3. Deploy Primary Application
4. Deploy Canary Application
5. Deploy Redis
