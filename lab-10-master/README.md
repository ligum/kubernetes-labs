# Kubernetes Workshop
Lab 10: Configuring Autoscaling

---

## Instructions

### Check current cluster nodes

 - Check the current number nodes in your cluster
```
kubectl get nodes
```

### Deploy a Sample App

 - Deploy the application comprised from A Deployment and A service
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-10/raw/master/Apache_Deployment_And_Service.yaml
```

 - Ensure that the deployment resource was created successfully
```
kubectl get deployments
```

 - Ensure the application is up and running
```
kubectl get pods
```

 - Ensure the application service was deployed successfully
```
kubectl get svc
```

### Create an HPA resource

 - Create a **AutoScale**\**HPA** resource to scales up when CPU exceeds 50% of the allocated container resource
```
kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=5
```

 - Ensure the HPA resource was created successfully
```
kubectl get hpa
```

### Generate load to trigger scaling

 - In a **new terminal** run the following command to drop into a shell on a new container
```
kubectl run -i --tty load-generator --image=busybox /bin/sh
```

 - Execute a while loop to continue getting http:///php-apache (then minimize the terminal)
```
while true; do wget -q -O - http://php-apache; done
```

 - In the previous terminal watch the changes of HPA with the following command
```
kubectl get hpa --watch
```

 - You can check the running pods as well
```
kubectl get pods
```
 
### Edit HPA configuration

 - Edit the **HPA** resource to increment the **maxReplicas** up to 50 and the **minReplicas** to 3
```
kubectl edit hpa php-apache
```

 - Watch the HPA with the following command to see how the application is beeing scaled
```
kubectl get hpa --watch
```

 - You can check the running pods as well
```
kubectl get pods
```

### Check current cluster nodes

 - Check the current nodes of your cluster and see that the nodes have been added
```
kubectl get nodes
```

### Stop the load to stop the scaling process

 - Stop (Ctrl + C) the load test that was running in the other terminal. 
 
 - You will notice that HPA will slowly bring the replica count to min number based on its configuration.
 
 - Also you will notice that the node count going down as well.

 
### Cleanup

 - List existing resources
```
kubectl get all
```

 - Delete existing resources
```
kubectl delete all --all
```

 - List existing resources
```
kubectl get all
```
