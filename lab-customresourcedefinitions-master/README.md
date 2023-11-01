# Kubernetes Workshop
Lab: Custom Resource Definitions

---

## Instructions

 - Create a working directory for the lab
```
mkdir ~/lab-crd
cd ~/lab-crd/
```

 - Create a file describing your CRD:
```
cat <<EoF > ~/lab-crd/resourcedefinition.yaml
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  # name must match the spec fields below, and be in the form: <plural>.<group>
  name: crontabs.stable.example.com
spec:
  # group name to use for REST API: /apis/<group>/<version>
  group: stable.example.com
  # list of versions supported by this CustomResourceDefinition
  versions:
    - name: v1
      # Each version can be enabled/disabled by Served flag.
      served: true
      # One and only one version must be marked as the storage version.
      storage: true
  # either Namespaced or Cluster
  scope: Namespaced
  names:
    # plural name to be used in the URL: /apis/<group>/<version>/<plural>
    plural: crontabs
    # singular name to be used as an alias on the CLI and for display
    singular: crontab
    # kind is normally the CamelCased singular type. Your resource manifests use this.
    kind: CronTab
    # shortNames allow shorter string to match your resource on the CLI
    shortNames:
    - ct
EoF
```

 - Create your "crontabs.stable.example.com" CRD:
```
kubectl apply -f ~/lab-crd/resourcedefinition.yaml
```

 - Ensure that the CRD was successfully created:
```
kubectl get crd crontabs.stable.example.com
```

 - Describe your CRD:
```
kubectl describe crd crontabs.stable.example.com
```

 - Optionally you can retrieve it directly from the Kubernetes API:
```
kubectl proxy --port=8080 --address='0.0.0.0' --disable-filter=true
curl -i 127.0.0.1:8080/apis/apiextensions.k8s.io/v1beta1/customresourcedefinitions/crontabs.stable.example.com
```

 - Create a manifest for a "CronTab" object from your CRD:
```
cat <<EoF > ~/lab-crd/my-crontab.yaml
apiVersion: "stable.example.com/v1"
kind: CronTab
metadata:
  name: my-new-cron-object
spec:
  cronSpec: "* * * * */5"
  image: my-awesome-cron-image
EoF
```

 - Create the "CronTab" object:
```
kubectl apply -f ~/lab-crd/my-crontab.yaml
```

 - Retrieve your "CronTab" object:
```
kubectl get crontab
kubectl get ct -o yaml
kubectl describe crontab
```

### Cleanup

 - List existent resources:
```
kubectl get crd crontabs.stable.example.com
kubectl get crontab my-new-cron-object
```

 - Delete existent resources:
```
kubectl delete crontab my-new-cron-object
kubectl delete crd crontabs.stable.example.com
```
