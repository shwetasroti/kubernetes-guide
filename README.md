# kubernetes-guide
![image](https://user-images.githubusercontent.com/96919604/150732469-14f9090a-4a02-48ed-8cc5-78dcddb25db7.png)


# Get Worker Node Status
kubectl get nodes

# Get Worker Node Status with wide option
kubectl get nodes -o wide
Create a Pod
Create a Pod
# Template
kubectl run <desired-pod-name> --image <Container-Image> --generator=run-pod/v1

# Note:
With Kubernetes 1.18 version, there is lot clean-up to kubectl run command.
The below will suffice to create a Pod as a pod without creating deployment. We dont need to add --generator=run-pod/v1
kubectl run my-first-pod --image <imagename>/kubenginx:1.0.0
  
# List Pods
kubectl get pods

# Alias name for pods is po
kubectl get po
# List Pods with wide option
kubectl get pods -o wide
  
# To get list of pod names
kubectl get pods

# Describe the Pod
kubectl describe pod <Pod-Name>
kubectl describe pod my-first-pod 

# Delete Pod
kubectl delete pod <Pod-Name>
kubectl delete pod my-first-pod
  
# Expose Pod with a Service
Expose pod with a service (NodePort Service) to access the application externally (from internet)
kubectl run <desired-pod-name> --image <Container-Image> --generator=run-pod/v1
kubectl run my-first-pod --image <imagename>/kubenginx:1.0.0 --generator=run-pod/v1

# Expose Pod as a Service
kubectl expose pod <Pod-Name>  --type=NodePort --port=80 --name=<Service-Name>
kubectl expose pod my-first-pod  --type=NodePort --port=80 --name=my-first-service

# Get Service Info
kubectl get service
kubectl get svc

# Get Public IP of Worker Nodes
kubectl get nodes -o wide
Access the Application using Public IP
http://<node1-public-ip>:<Node-Port>

# Note
If target-port is not defined, by default and for convenience, the targetPort is set to the same value as the port field.
# Below command will fail when accessing the application, as service port (81) and container port (80) are different
kubectl expose pod my-first-pod  --type=NodePort --port=81 --name=my-first-service2     

# Expose Pod as a Service with Container Port (--taret-port)
kubectl expose pod my-first-pod  --type=NodePort --port=81 --target-port=80 --name=my-first-service3

# Get Service Info
kubectl get service
kubectl get svc

# Get Public IP of Worker Nodes
kubectl get nodes -o wide
Access the Application using Public IP
http://<node1-public-ip>:<Node-Port>
  
# Interact with a Pod
Verify Pod Logs
# Get Pod Name
kubectl get po

# Dump Pod logs
kubectl logs <pod-name>
kubectl logs my-first-pod

# Stream pod logs with -f option and access application to see logs
kubectl logs <pod-name>
kubectl logs -f my-first-pod

# Reference: https://kubernetes.io/docs/reference/kubectl/cheatsheet/

# Connect to Nginx Container in a POD
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec -it my-first-pod -- /bin/bash

# Execute some commands in Nginx container
ls
cd /usr/share/nginx/html
cat index.html
exit
Running individual commands in a Container
kubectl exec -it <pod-name> env

# Sample Commands
kubectl exec -it my-first-pod env
kubectl exec -it my-first-pod ls
kubectl exec -it my-first-pod cat /usr/share/nginx/html/index.html

# Step-06: Get YAML Output of Pod & Service
kubectl get pod my-first-pod -o yaml   

# Get service definition YAML output
kubectl get service my-first-service -o yaml   

# Step-07: Get all Objects in default namespace
kubectl get all

# Delete Services
kubectl delete svc my-first-service
kubectl delete svc my-first-service2
kubectl delete svc my-first-service3

# Delete Pod
kubectl delete pod my-first-pod

# Get all Objects in default namespace
kubectl get all
  
  
# Flow Chart
  ![k8s](https://user-images.githubusercontent.com/96919604/151666716-0c7689bc-d240-41af-8099-c1037607a394.png)

