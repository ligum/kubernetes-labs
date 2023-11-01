# Kubernetes Workshop
Lab 11: Working with StatefulSets

---

## Instructions

### Deploy the StatefulSet

 - Create the a headless service for the **StatefulSet**
```
kubectl create -f https://gitlab.com/sela-kubernetes-workshop/lab-11/raw/master/service.yaml
```

 - Ensure the service was created successfully
```
kubectl get svc
```

 - Create the **StatefulSet**
```
kubectl create -f https://gitlab.com/sela-kubernetes-workshop/lab-11/raw/master/statefulset.yaml
```

 - Ensure the **StatefulSet** was created successfully
```
kubectl get statefulsets
```

 - Inspect the **StatefulSet** pods
```
kubectl get pods -l="app=nginx"
```

 - Inspect the **StatefulSet**'s **PVC**s
```
kubectl get pvc
```

 - Inspect the **StatefulSet**'s **StorageClass**
```
kubectl get storageclass
```

 - Inspect the **StatefulSet**'s **PV**s
```
kubectl get pv
```

### Scale up the StatefulSet

 - Edit the **StatefulSet** replicas to scale to 5 instances
```
kubectl edit statefulset web
```

 - Track the **StatefulSet** pods to see how the ReplicaSet scales to 5 replicas
```
kubectl get pods -l="app=nginx" --watch
```

 - Inspect the **StatefulSet** pods
```
kubectl get pods -l="app=nginx"
```

 - Inspect the **StatefulSet** resource
```
kubectl get statefulset web
```

### Scale down the StatefulSet

 - Edit the **StatefulSet** replicas to scale to 2 instances
```
kubectl edit statefulset web
```

 - Track the **StatefulSet** pods to see how the **ReplicaSet** scale down to 2 replicas
```
kubectl get pods -l="app=nginx" --watch
```

 - Inspect the **StatefulSet** pods
```
kubectl get pods -l="app=nginx"
```

 - Inspect the **StatefulSet** resource
```
kubectl get statefulset web
```

### Update a StatefulSet

 - Edit the **StatefulSet** replicas and update the pod image using the command
 ```
kubectl edit statefulset web
```
 Replacing the container like so
```
Replace:  gcr.io/google_containers/nginx-slim:0.8
With:     gcr.io/google_containers/nginx-slim:0.26
```


 - Track the **StatefulSet** update
```
kubectl rollout status statefulset web
```

 - Inspect the pods to ensure that the pod image was updated
```
kubectl describe pod web-0 | grep Image:
```
```
kubectl describe pod web-1 | grep Image:
```

### Rollback a StatefulSet

 - Rollback the **StatefulSet** update by run the command below
```
kubectl rollout undo statefulset web
```

 - Track the **StatefulSet** update process
```
kubectl rollout status statefulset web
```

 - Inspect the **StatefulSet** pods to check the used image
```
kubectl describe pod web-0 | grep Image:
```
```
kubectl describe pod web-1 | grep Image:
```

### Cleanup

 - List existing resources
```
kubectl get all
```

 - Delete the PVC's
```
kubectl delete pvc --all
```

 - Delete another resources
```
kubectl delete all --all
```

 - List existing resources
```
kubectl get all
```