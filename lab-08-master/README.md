# Kubernetes Workshop
Lab 08: Running Pods as DaemonSets

---

## Instructions

### Deploy a DaemonSet

 - We are going to create a **DaemonSet**, but before we will that please survey  the **DaemonSet** YAML definition:
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-08/raw/master/daemonset.yaml
```

- Create the DaemonSet from the **daemonset.yaml** file:
```
kubectl create -f https://gitlab.com/sela-kubernetes-workshop/lab-08/raw/master/daemonset.yaml
```

 - List the existing **DaemonSets**:
```
kubectl get ds
```

### Add a Label to Cluster Nodes

 - List the cluster's nodes in order to get thier names
```
kubectl get nodes
```

 - Add the label "app=logging-node" to the first node from the previous command:
```
kubectl label node <Node-Name> app=logging-node
```

 - List the existing **Daemonsets**
```
kubectl get ds
```

 - Add the label "app=logging-node" to the second node:
```
kubectl label node <node-name> app=logging-node
```
Ensure that both of the nodes have the "logging-node" label:
```
kubectl get nodes -l app=logging-node
```
 - List the existing **Daemonsets**
```
kubectl get ds
```

 - Describe Pods to ensure each Pod is deployed in a different node:
```
kubectl describe pods | grep Node:
```

### Remove a Node Label

 - List the cluster nodes in order to get thier names:
```
kubectl get nodes
```

 - Remove the label "app=logging-node" from one of the nodes:
```
kubectl label node <Node-Name> app-
```

 - List the existing **Daemonsets**
```
kubectl get ds
```

 - Describe the remaining Pod and checkout on which node it is running on
```
kubectl describe pods
```

### Cleanup

 - List the existing resources
```
kubectl get all
```

 - Delete the existing resources
```
kubectl delete all --all
```

 - List the existing resources
```
kubectl get all
```
