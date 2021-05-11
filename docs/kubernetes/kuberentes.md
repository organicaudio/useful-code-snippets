# Kuberentes overview

Kubernetes (K8s) allows to deploy multiple containers on one or multiple host systems. The [offial documentation of k8s](https://kubernetes.io/docs/) is outstanding. There is also a [interactive tutorial](https://kubernetes.io/docs/tutorials/kubernetes-basics/). There is also the really nice video [What is Kuberenetes - Techworld with NaNa](https://www.youtube.com/watch?v=VnvRFRk_51k) which gives an nicely animated overview of kubernetes.

outline of features:
- one master node and multiple worker nodes
- creates self-healing clusters 
- allows rolling upgrade and rollback
- secret management and encapsulation via namespaces

## terms

Master node:
- API server
  - web ui (dashboard)
  - kubectl
  - API
- Controller Manager - keep track of state on workers
- etcd DB - saves state of workers
- Scheduler - placement of pod based on load and other factors

Worker node:
- kubelet (kubernetes node agent)
- Docker (or containerd compliant software)
- kube-proxy (supported modes: user space, iptables, ipvs)

base objects:
- pod - to run container
- service - to access pods
- volume - to persists data from pods
- namespace - to separate objects 

Pods:
- are one or multiple containers which
- share a unique network IP Address
- "Containers should only be scheduled together in a single Pod if they are tightly coupled and need to share resources such as disk."

controllers allow:
1. fail over
2. scaling
3. load balancing

Kind of controllers:
- RepilcaSet: ensures that a specified number of pods is runnning in a node (needs another controller as wrapper like deployment)
- Deployment: declarative describe how to create and update instances (self-healing mechanism)
- DaemonsSets: ensures that all nodes run a specific copy of a pod (1 DaemonSet - 1 Pod - X nodes).
- Jobs: supervisor for pods which do batch jobs
- Services: allow communication between deployment controllers

Services:
- allows to manage how the pods can be accessed
- defines a logical set of pods 
- pods are selected via a LabelSelector 
- modes:
    - ClusterIP (default): pods can only communicate within k8s cluster over there IP
    - NodePort: pods can be accessed through the node ip and the so called NodePort
    - load balancer: to expose application to the internet
    - ExternalName: expose a service by a name


Labels:
- added to objects like pods, services, deployments
- key-value pairs to identify attributes of objects

Selectors:
- allows to select objects by a label
- equality-based: `=` and `!=`
- set-based: `IN`, `NOTIN`, `EXISTS`
  
Namespaces:
- allows multiple virtual clusters on the same physical host
- there is a default namescpace

## install

- Install Docker like in the [official documentation](https://docs.docker.com/engine/install/) or use the install script `curl -sSL https://get.docker.com | sh` which might be easier
- [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- install [auto completion for kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enable-kubectl-autocompletion): `kubectl completion bash >/etc/bash_completion.d/kubectl` *might get permission issues with this command. Than write it  to ~/kubectl and mv it with sudo to the target folder*
- if you want to test stuff on your local machine  [install minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/#before-you-begin). **Note the 'Before you begin' section which shows you how to check for a supervisor.** If you do not have one install one like VirtualBox.

## kubectl cli

[kubectl reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
[cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)


basic commands:
- `kubectl cluster-info` list masternodes and worker nodes
- `kubectl apply -f FILENAME` create/updates the defined objects in the given yaml file.
- `kubectl get all`
    - `kubectl get nodes`
    - `kubectl get services`
    - `kubectl get deployments`
    - `kubectl get rs` list replica sets
    - `-l <label>` to load only resources with the given label

update pod:
- `kubectl set image deployments/<POD_NAME> <POD_NAME>=<IMAGE>:<VERSIONTAG>` set image of a pod to a newer version
- `rubectl rollout undo deployments/<POD_NAME> ` rollback to previous version

create resources without k8s file:
- `kubectl run <POD_NAME> --image=<IMAGE>` starts a pod with the given image
- `kubectl create deployment <deployment_name/POD_NAME> --image=<IMAGE>` creates a deployment which starts a pod with the given image
- `kubectl expose <POD_NAME> --type=NodePort --port=80` creates a service on port 80 of the node.
- `kubectl label pod <POD_NAME> <labelKey=labelValue>` cretes a label on a pod
- `kubectl scale deployments/<POD_NAME> --replicas=4` creates a replication set

debug pod:
- `kubectl proxy ` proxy into a cluster even when no services are exposed. Pods are accessible via there pod name or there internal ip address. Terminate with ctrl + c.
- `kubectl describe <node/pods/deployment>`
- `kubectl kubectl logs <POD_NAME>`
- `kubectl exec <POD_NAME>` - execute a command on a container in a pod
- `kubectl exec -ti <POD_NAME> bash` open bash in container
## minicube cli

- `minicube start`
- `minicube service <POD_NAME>` shows the service in the browser

## k8s yaml file (manifests)

[Overview](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)

Required fields:
- apiVersion: kubernetes API version you use
- kind: type of object (e.g. Deployment, Pod)
- metadata: fields that allow to uniquely identify the object (name, UID, optional namespace)
- spec: the state you desire for the object. The spec fields are different for ever object and can be look up under [kubernetes api reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#container-v1-core).