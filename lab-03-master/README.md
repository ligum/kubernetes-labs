# Kubernetes Workshop
Lab 03: Deploy and Upgrade a Single App

---

## Instructions

### Deploy application using deployments

 - List existing Deployments
```
kubectl get deployments
```

 - List existing Pods
```
kubectl get pods
```

 - Inspect the Deployment's definition
```
curl   https://gitlab.com/sela-kubernetes-workshop/lab-03/raw/master/frontend-deployment.yaml --output frontend-deployment.yaml
```
```
cat frontend-deployment.yaml
```

 - Create the Deployment's resource
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-03/raw/master/frontend-deployment.yaml
```

 - List existing Deployments
```
kubectl get deployments
```

 - List existing Pods
```
kubectl get pods
```

 - Inspect the Pods' images
```
kubectl describe pods
```

### Rolling a Zero-Downtime update

 - Export the deployment definition to a file named **frontend-deployment-v2.yaml** by using the following command:
```
cat frontend-deployment.yaml > frontend-deployment-v2.yaml
```

 - Edit the exported definition file by changing the container image to refer it to a new version of the image
```
nano frontend-deployment-v2.yaml
```
```
Action:
-----------
Replace: selaworkshops/sentiment-analysis-frontend:v1
With: selaworkshops/sentiment-analysis-frontend:v2
```

 - Apply your changes to start the rolling upgrade sequence:
```
kubectl apply -f frontend-deployment-v2.yaml
```

 - We can check the status of the rollout using the following command:
```
kubectl rollout status deployment frontend
```

 - Inspect the pods' images
```
kubectl describe pods
```

### Rolling back to a previous state

 - Inspect the rollout history using the following command:
```
kubectl rollout history deployment frontend
```

 - Rollback to the first revision of the Deployment:
```
kubectl rollout undo deployment frontend --to-revision=1
```

 - We can check the status of the rollout using the following command:
```
kubectl rollout status deployment frontend
```

 - Inspect the pods' images
```
kubectl describe pods
```

### Cleanup

 - List all existing resources
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
