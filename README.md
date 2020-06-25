## k8s limitrange cpu memory storage per namespace



#### create namespace staging-zeus

kubectl apply -f namespace.yml

#### apply limit for namespace staging-zeus
kubectl apply -f limitrange.yml


#### check limit in namespace staging-zeus
kubectl describe namespaces staging-zeus

Name:         staging-zeus
Labels:       name=staging-zeus
Annotations:  Status:  Active

Resource Limits
 Type                   Resource  Min    Max   Default Request  Default Limit  Max Limit/Request Ratio
 Container              cpu       100m   800m  200m             200m           -
 Container              memory    100Mi  1Gi   200Mi            200Mi          -
 PersistentVolumeClaim  storage   1Gi    5Gi   -                -              -



#### test deploy container with over limit cpu and ram

 kubectl apply -f deployment-test-limit.yml


#### check 
kubectl get deployment staging-app-test -o yaml -n staging-zeus

 - lastTransitionTime: "2020-06-25T03:15:19Z"
    lastUpdateTime: "2020-06-25T03:15:19Z"
    message: 'pods "staging-app-test-6879c486bc-hzwq7" is forbidden: [maximum cpu
      usage per Container is 800m, but limit is 950m., maximum memory usage per Container
      is 1Gi, but limit is 1200Mi.]'
    reason: FailedCreate
    status: "True"
    type: ReplicaFailure
