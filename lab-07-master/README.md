# Kubernetes Workshop
Lab 07: Running Jobs and CronJobs
---

## Instructions

### Run Single Job

 - Please create a **Job** to calculate prime numbers between 0 and 110, but before that please survey the job's definition:
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/single-job.yaml
```

 - Please create the single **Job**: 
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/single-job.yaml
```

 - Please list existing **Jobs**
```
kubectl get jobs
```

 - Please list existing **Pods**:
```
kubectl get pods
```

 - Please inspect the **Pod**'s logs:
```
kubectl logs <Pod-Id>
```

### Run Sequentially Jobs

 - Please create the same job but multiple times (Sequentially), check the job definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/sequentially-job.yaml
```

 - Open a new terminal session and watch how the jobs are created 
```
kubectl get pods -l app=primes-sequentially --watch
```

 - Create the **Job**:
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/sequentially-job.yaml
```

 - Please list the existing **Jobs**
```
kubectl get jobs/primes-sequentially
```

 - Please list the existing **Pods**:
```
kubectl get pods
```

### Run Parallel Jobs

 - Please create the same job but multiple times (in Parallel), check the job's definition:
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/parallel-job.yaml
```

 - In a new terminal watch how the jobs are beeing created:
```
kubectl get pods -l app=primes-parallel --watch
```

 - Create the **Job**: 
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/parallel-job.yaml
```

 - Please list the existing **Jobs**:
```
kubectl get jobs/primes-parallel
```

 - Please list the existing **Pods**:
```
kubectl get pods
```

### Run a Basic CronJob

 - Please create a basic CronJob that would write a Hello World every minute, check the job definition
```
curl https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/cron-job.yaml
```

 - Create the **CronJob** 
```
kubectl apply -f https://gitlab.com/sela-kubernetes-workshop/lab-07/raw/master/cron-job.yaml
```

 - Wait until the **CronJob** is triggered
```
kubectl get pods --watch
```

 - Check the a **CronJob**'s **Pod** output:
```
kubectl logs <pod-id>
```

### Cleanup

 - List the existing resources:
```
kubectl get all
```

 - Delete the existing resources:
```
kubectl delete all --all
```

 - List the existing resources:
```
kubectl get all
```
