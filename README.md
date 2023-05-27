# kubernetes

```
Kubernetes is an opensource cloud native container orchestrator
```

### kubenetes commands 


Most used Kubernetes commands :

```
Syntax :  kubectl action resources 

* kubectl get nodes  
* kubectl get nodes -o wide
* kubectl cluster-info 
* kubectl api-versions
* kubectl api-resources 
* kubectl --help 
```

How do you deploy a kubernetes resource ?

```
kubectl apply -f fileName.yml 
```

How do you delete a kubernetes resource ?

```
kubectl delete -f fileName.yml 
```

### PS : 

```
Kubernetes resources are indendation specific and are idempotent.
```

### Kubernetes Configuration :
```
    Kubectl will try to use the config resides in ~/.kube/config file 
```

## K8 resources can be created by imperative commands or with the declaratvie approch ( VCS )

#### Resources :
```
    1) PODS
    2) ENV 
    3) CMD 
    4) ConfigMap 
    5) Secret 
    
    6) SETS  
        a) ReplicaSets        
        b) Deployments
        c) DaemonSets
        d) StatefulSets

    7) Health Checks
        a) Readiness Probe 
        b) Liveliness Probe 
        c) Startup Probe     
    8) Resource Utilization   ( CPU, Memory, Page )
        a) Requests
        b) Limits

    9) NameSpace 
    
   10) Services
        a) ClusterIP        ( Limits the visibility of the service only with in the cluster )
        b) LoadBalancer     ( Gives the visbility to public, outside of the cluster )
        c) NodePort         ( Opens the port directly on the NODE )
        d) External         ( It's just like a CNAME to a long name to service in the K8 Cluster )

    11) Pod Priority & Pre-emption 


### What is a page: 

```
In OS, processes are divided into equal parts called pages, and main memory is also divided into equal parts and each part is called a frame. Each page gets stored in one of the frames of the main memory whenever required. So, the size of a frame is equal to the size of a page.
```

``` 
### <u> OpenShift :  </u>
It's a RedHat Flavored K8's. Majorly used for Kubernetes Solution on Data Centers
```
    Linux ---> RedHat ( ES )
          ---> CentOS ( CS )

    K8   ---> OpenShift  ( ES ) 
         ---> Kubernetes ( CS )
             ( EKS , GKE )

```
## Probes

### Liveliness Prode:
```
The kubelet uses liveness probes to know when to restart a container. For example, liveness probes could catch a deadlock, where an application is running, but unable to make progress. Restarting a container in such a state can help to make the application more available despite bugs.
```
### Readiness Probe: 
```
The kubelet uses readiness probes to know when a container is ready to start accepting traffic. A Pod is considered ready when all of its containers are ready. One use of this signal is to control which Pods are used as backends for Services. When a Pod is not ready, it is removed from Service load balancers.
```


### Resource Allocation :
```
It's always recommended to give a maximum of 80% of the nodes capability to a pod.

t3.Medium : 2 CPU , 4 GB Memory 

2 - 0.4 = 16 Core 
4 - 1.2 = 2.8 Mem 
```


### Pod Priority & Preemption 

```
Pods can have priority. Priority indicates the importance of a Pod relative to other Pods. If a Pod cannot be scheduled, the scheduler tries to preempt (evict) lower priority Pods to make scheduling of the pending Pod possible.

Pob Preemption: Allows Cluster to evict the low priority pods, so that they can be evict the low priority pods to accomodat the high priority pods.

  
  --> The higher the value, the higher the priority

Ref : https://mohaamer5.medium.com/kubernetes-pod-priority-and-preemption-943c58aee07d

```

### How to create a priority class ?

```
    apiVersion: scheduling.k8s.io/v1
    kind: PriorityClass
    metadata:
    name: high-priority
    value: 1000000
    globalDefault: false
    description: "This priority class should be used for XYZ Customers pods only."

```

### REPLICA SET : 
```
A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.
```

### What is a package manager is centos ?  YUM 

### What is a package manager in K8 ? 
```HELM``` 



### How to install ingress controller ?

```
Ref: https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-helm/  

Here are the steps to install ingress controller :

$  helm repo add nginx-stable https://helm.nginx.com/stable
$  helm repo update 
$  helm install my-release nginx-stable/nginx-ingress

```


### How to create a helm chart ?

$ helm create .   

### Here is how the structre of the helm chart looks like

```

sample-helm-chart/
├── charts                  
├── Chart.yaml                         // Chart Metadata file   
├── templates                          // All the templated resources would be placed here
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── serviceaccount.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml                       // Default values of the char would placed.

``` 


### How to install our install our own helm chart ?

```
$ helm install chartName ./chartLocation  

$ helm list 

$ helm upgrade chartName ./chartLocation

```


Why are we using HELM Charts ?

```
helm charts helps you in keeping the code DRY, which means you can paramterize the whole K8 Manifest file and there by providing an opportunity to create the files once and use it n number times by supplying different values.yml file  
```

```
### How to uninstall the chart ?

```
$ helm uninstall chartName   

$ helm list 

$ helm upgrade chartName ./chartLocation




### Deployment Strategy in Kubernetes : 

deployment can be done in 2 ways  :

```
    1) Rolling update 
    2) Recreate 
``` 


### Ingress Controller Installation 

```
    $ git clone https://github.com/nginxinc/kubernetes-ingress.git --branch v3.0.2
    $ cd kubernetes-ingress/deployments/helm-chart
    $ helm repo add nginx-stable https://helm.nginx.com/stable
    $ helm repo update
    $ helm install ng-ingress  nginx-stable/nginx-ingress
    $ helm list

``` 