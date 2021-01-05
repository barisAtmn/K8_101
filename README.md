# KUBERNETES

Container orchestration

* Node(worker) : container runtime, kube-proxy, kubelet
* Master : api-server, etcd, controller, scheduler

Components;
- etcd
- kubelet
- container runtime
- controller
- scheduler
- api server
- kube-proxy

* Template
```
  apiVersion: 
  kind:
  metadata:
  spec:
```  

=> etcd is an open source distributed key-value store used to hold and manage the critical information that distributed
systems need to keep running.

==> api server : frontend for kubernetes

==> scheduler : responsible for distributing work to nodes

==> controller : brain behind of orchestration. makes decision when new nodes create.

==> container runtime: like docker, rkt

==> kubelet : agent runs on each nodes

==> kube-proxy:  maintains network rules on nodes. These network rules allow network communication to your Pods from network
sessions inside or outside of your cluster.

## MINIKUBE 

==> minikube start --driver=virtualbox

==> minikube start --driver=docker

==> minikube start --cpus 4 --memory 8192

==> minikube config set driver virtualbox


## DEPLOYMENT

* When a deployment is added to the cluster, it will automatically spin up the requested number of pods, and then monitor them.
If a pod dies, the deployment will automatically re-create it.

==> kubectl get deployments

==> kubectl expose deployment hello-node --type=LoadBalancer --port=8080

==> kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4

==> kubectl run redis --image=redis

==> kubectl run redis --image=redis123 --dry-run=client -o yaml > pod.yaml
==> kubectl apply -f pod.yaml

==> kubectl delete deployment hello-node

## POD

* pods are usually managed by one more layer of abstraction: the deployment. A deployment’s primary purpose is to declare
how many replicas of a pod should be running at a time.

* Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

* A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage/network resources, and a
specification for how to run the containers.

==> kubectl get pods

==> kubectl get po -o wide

==> kubectl describe po {name of pod}

==> kubectl edit pod redis

==> kubectl apply -f {file.yaml}

## NODE

* A node is the smallest unit of computing hardware in Kubernetes.

==> kubectl get nodes

==> kubectl get nodes -o wide


## REPLICASET

==> kubectl create -f replicaset.yaml

==> kubectl get replicaset

==> kubectl edit replicaset {myapp-replicaset} // on fly

==> kubectl scale replicaset {myapp-replicaset} --replicas=2



## ROLLOUT 

==> kubectl rollout history {deployment.apps/myapp-deployment}

==> kubectl rollout undo {deployment.apps/myapp-deployment}

==> kubectl rollout status {deployment.apps/myapp-deployment}


## SERVICE 

==> kubectl get services

==> kubectl delete service hello-node

==> kubectl get services

## INGRESS

* By default, Kubernetes provides isolation between pods and the outside world. If you want to communicate with a service running
in a pod, you have to open up a channel for communication. This is referred to as ingress.


### NOTES

==> What's the difference between a Service and a Deployment in Kubernetes?

- A deployment is responsible for keeping a set of pods running.
- A service is responsible for enabling network access to a set of pods.