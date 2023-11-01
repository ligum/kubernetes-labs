# Kubernetes Workshop
Lab 02: Creating and scaling your first pod

---

## Instructions

### Create a Namespace

 - Create a namespace definiton by creating a file called **"namespace.yaml"** using the command below:
```
cat << EOF > ~/namespace.yaml 
apiVersion: v1
kind: Namespace
metadata:
  name: dev
EOF
```

 - Create the namespace using kubectl
```
kubectl create -f namespace.yaml
```

 - Check that the namespace was created successfully
```
kubectl get namespaces
```

 - Set the created namespace as the default namespace
```
kubectl config set-context --current --namespace=dev
```

---

### Creating Our First Pod

 - Inspect the Pod's definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-02/raw/master/echoserver-pod.yaml
```

 - List current existing Pods
```
kubectl get pods
```

 - Create the following Pod in the manifest file:
```
kubectl create -f https://gitlab.com/sela-kubernetes-workshop/lab-02/raw/master/echoserver-pod.yaml
```

 - List current existing Pods
```
kubectl get pods
```

### Creating Our First ReplicaSet

 - Inspect the ReplicaSet's definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-02/raw/master/echoserver-rs.yaml
```

 - List current existing ReplicaSets
```
kubectl get replicasets
```

 - Create the following ReplicaSet
```
kubectl create -f https://gitlab.com/sela-kubernetes-workshop/lab-02/raw/master/echoserver-rs.yaml
```

 - List current existing ReplicaSets
```
kubectl get rs
```

 - List current existing pods
```
kubectl get pods
```

### Scaling our application using ReplicaSets

 - Inspect the current ReplicaSet
```
kubectl describe rs echoserver
```

 - Edit the ReplicaSet to update "replicas" from "3" to "2"
```
kubectl edit rs echoserver
```

 - List current existing ReplicaSets
```
kubectl get rs
```

 - List current existing Pods
```
kubectl get pods
```

### Cleanup

 - List existing resources in your namespace
```
kubectl get all
```

 - Delete all existing resources
```
kubectl delete all --all
```

 - List existing resources to ensure that the environment is clean
```
kubectl get all
```
