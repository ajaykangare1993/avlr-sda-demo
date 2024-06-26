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
    
2. Deploy Primary Application

   kubectl apply -f ingress-nginx primary-deploy.yaml
   kubectl apply -f ingress-nginx primary-service.yaml
   kubectl apply -f ingress-nginx primary-ingress.yaml
   
3. Deploy Canary Application

   kubectl apply -f ingress-nginx canary-deploy.yaml
   kubectl apply -f ingress-nginx canary-service.yaml
   kubectl apply -f ingress-nginx canary-ingress.yaml
 
5. Deploy Redis

   kubectl apply -f ingress-nginx redis-conf.yaml
   kubectl apply -f ingress-nginx redis-pvc.yaml
   kubectl apply -f ingress-nginx redis-deploy.yaml
   kubectl apply -f ingress-nginx redis-service.yaml
   kubectl apply -f ingress-nginx redis-ingress.yaml

<img width="893" alt="image" src="https://github.com/ajaykangare1993/avlr-sda-demo/assets/169615774/32e9e1bf-cf4c-4bcd-b98e-147bbe936490">
<img width="1470" alt="image" src="https://github.com/ajaykangare1993/avlr-sda-demo/assets/169615774/afdf42ab-68b2-4264-8502-9428fc649a76">
<img width="762" alt="image" src="https://github.com/ajaykangare1993/avlr-sda-demo/assets/169615774/cb7111b3-5aa0-4397-8dda-f2cfb65b853e">


