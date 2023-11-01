# Kubernetes Workshop
Lab 06: Using ConfigMaps and Secrets

---

## Instructions

### Create ConfigMaps and Secrets from CLI

 - Create a basic ConfigMap to store a shared variable
```
kubectl create configmap language --from-literal=LANGUAGE=English
```

 - Create a basic Secret to store a shared API Token
```
kubectl create secret generic apikey --from-literal=API_KEY=123–456
```

 - List existing ConfigMaps 
```
kubectl get ConfigMaps 
```

 - List existing Secrets
```
kubectl get secrets
```

 - Inspect the created ConfigMap
```
kubectl describe configmap language
```

 - Inspect the created Secret
```
kubectl describe secret apikey
```

 - Please create a Pod to use the variables that we hace created
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/cli-test-pod.yaml
```

 - Inspect the Pod's definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/cli-test-pod.yaml
```

 - Please see the Pod's output
```
kubectl logs cli-test
```
```
kubectl logs cli-test | grep LANGUAGE
kubectl logs cli-test | grep API_KEY
```

### Create ConfigMap from YAML manifest and use it as file

 - Please create a ConfigMap resource (index.html and .css file)
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/file-configmap.yaml
```

 - Inspect the ConfigMap definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/file-configmap.yaml
```

 - Create a Deployment to run Nginx and use the ConfigMap files 
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/file-deployment.yaml
```

 - Inspect the Deployment definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/file-deployment.yaml
```

 - Create a service to expose the web server
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/file-service.yaml
```

 - Inspect the service definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-06/raw/master/file-service.yaml
```

 - List existing services
```
kubectl get services --watch
```

 - Wait a while until the "LoadBalancer" service finished beeing created. Then browse to the web application
```
http://<service-ip>:80
```

### Update ConfigMaps and access to container pods

 - Please update the HTML file in the previous ConfigMap resource
```
kubectl edit configmap demo-app-content
```

 - Update the welcome message:
```
From: Hello from my ConfigMap!
To: Hello from my updated ConfigMap!!!
```

 - Get the Pod's id
```
kubectl get pods --field-selector status.phase=Running --no-headers | cut  -d " " -f 1
```

 - Access to the Pod's container
```
kubectl exec -it <pod-id> -- /bin/sh 
```

 - Inspect the html file content and exit from the container
```
cat /usr/share/nginx/html/index.html
```
```
exit
```

 - Browse to the web application to see the changes:
```
http://<service-ip>:80
```

 - Please delete the current Pod, kubernetes will provide a new one:
```
kubectl delete pod <pod-id>
```

 - Browse to the web application again
```
http://<service-ip>:80
```

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