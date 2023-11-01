# Kubernetes Workshop
Lab 04: Creating a Load Balancer Service

---

## Application Architecture

<img alt="voting-app-architecture" src="voting-app-architecture.png"  width="60%" height="60%">


## Instructions

 - Clone the lab's repository
```
git clone https://gitlab.com/sela-kubernetes-workshop/lab-04.git ~/lab-04
```
```
cd ~/lab-04
```

 - Please list the Deployments resources form within the git's folder:
```
ls -l ~/lab-04/k8s-deployments/
```

 - Create the Deployment resources in k8s-deployments folder
```
kubectl apply -f ~/lab-04/k8s-deployments/
```

 - Please list the existing Deployments
```
kubectl get deployments
```

 - Please list the existing Pods
```
kubectl get pods
```

 - The worker Pod will faile because there is still no connection between the pods
```
NAME                      READY   STATUS             RESTARTS   AGE
db-5696969744-sjrsj       1/1     Running            0          6m
redis-556f489c7c-7xjgx    1/1     Running            0          6m
result-84868df65f-dmjvh   1/1     Running            0          6m
vote-6df549f448-58kkk     1/1     Running            0          6m
worker-777dc9c586-bb65h   0/1     CrashLoopBackOff   5          6m
```

 - Please list the existing services 
```
kubectl get services
```
- As you can see, there are no services designated for the Deployments

 -Please survey The **"db"** and **"redis"** services Yaml files, eventually they should be accessible only within the cluster, therefor we will configure them as **"ClusterIP"** services entities - for example:
```
apiVersion: v1
kind: Service
metadata:
  name: db
spec:
  type: ClusterIP
  ports: 
  - port: 5432
    targetPort: 5432
  selector:
    app: db
```

 - Please create both of the services
```
kubectl apply -f ~/lab-04/k8s-services/db-service.yaml
```
```
kubectl apply -f ~/lab-04/k8s-services/redis-service.yaml
```

 - The **"result"** and **"vote"** services should be accessible from outside the cluster, therefor we will configure them as **"LoadBalancer"** services like so:
```
apiVersion: v1
kind: Service
metadata:
  name: vote
spec:
  type: LoadBalancer
  ports:
  - name: "vote-service"
    port: 5000
    targetPort: 80
  selector:
    app: vote
```

 - Please create both of the services:
```
kubectl apply -f ~/lab-04/k8s-services/result-service.yaml
```
```
kubectl apply -f ~/lab-04/k8s-services/vote-service.yaml
```

 - Please List the existing Services:
```
kubectl get services  --watch
```

 - Wait a while until the "Load Balancer" type services are finished of beeing created , the indication will be that they are no longer in a "Pending" status and will present an external IP.
 - Copy the external IPs of the "LoadBalancer" services to a notepad document.
 - Hold the ctrl button + C to exit from the watch status.
 - Once you are done, please insure that all the pods are in a running state.
```
kubectl get pods
```

 - Access the "**vote**" service and place your vote!
 
```
http://<vote-service-lb-ip>:5000
```

 - Access the "**result**" service and check the results:

```
http://<result-service-lb-ip>:5001
```

 - Delete the "**result**" and "**vote**" services
```
kubectl delete -f ~/lab-04/k8s-services/result-service.yaml
```
```
kubectl delete -f ~/lab-04/k8s-services/vote-service.yaml
```

 - Please list the existing pods
```
kubectl get pods
```

 - Please list the existing services
```
kubectl get services
```

 - Even though the application is up and running, without the services users would not be able to access the application

 
### Cleanup

 - List existing resources
```
kubectl get all
```

 - Delete all existing resources
```
kubectl delete all --all
```

 - List all existing resources
```
kubectl get all
```
