1. How to create a normal Node.js Hello World App, test it and dockerize it, all details are here:
   URL: https://github.com/shubham-arora-18/node-js-app
2. How to run kubernetes cluster on local system, How use docker image created in step 1 and deploy it on kubernetes cluster, all details are here:
   URL: https://github.com/shubham-arora-18/node-app-k8s
3. How to deploy kubernetes cluster created in step 2 and deploy it on terraform created EKS, all details here:
   URL: https://github.com/shubham-arora-18/eks-terraform-infra
4. How to add istio ingress controller to manage multiple apis deployed on the kubernetes cluster:
   1. Istio ingress controller can be used as an entry point loadbalancer to our kubernetes cluster.
   2. IstioArch1 and IstioArch2 Images show the architecture, where Istio ingress controller will be placed and will interact with internal kubernetes services.
   3. We now instead of defining our kubernetes services type as LoadBalancer/NodePort will define our services type as ClusterIp, this will disable any external    interaction with service. And all the interaction with these services would now go through Istio ingress controller.

   Steps to do it-> 

   1. Download istioctl.
   2. To install instio type command: istioctl install --set profile=demo -y   .
   3. Use the following URL for above two steps: https://istio.io/latest/docs/setup/getting-started/
   4. The above steps would create 3 pods under namespace istio-system, one for ingress, one for egress and one for control plane. It would also create 3 services, mapped to the already created pods. Note only the ingress service will have a public ip here, meaning it would be the only service that would be open to the world for communication. The rest 2 would get internal ips.
   5. At this point, for all the services added infront of your microservices pods, make their type = CLusterIp. This would make these services unavailable to be contacted bythe external world.(note: this step is not mandatory but preferred)
   6. Create a gateway resource on your eks cluster. For eg. you could configure this gateway to listen for http request on port 80 and https request on port 443.
   7. Create one virtual service for each service deployed in the kubernetes cluster. Here you can add configuration for domain/route to service mapping.

   Note: A walkthrough demonstration for all the above steps: https://www.youtube.com/watch?v=K73Q5bS4X6Y&t=1735s
