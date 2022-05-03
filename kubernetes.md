# What is Kubernetes

Container Orchestration Engine (COE) -
Top 3 COE

- Marathin by Apache Mesos - for Large enterprise, requires lot of compute, driven by developers
- Docker Swarm - for small org
- K8s - Large orgs, open source
  Others for small team sizes - rancher, nomad kubeadm init - on master to create k8s cluster

```
kubeadmin join -- token [] --doscpvery-token-ca-cert-hash to join any worker node into the cluster

kubeadm token

kubeadmin ungrade
```

## Pod

- grouping of containers
- why pod
  - group **very similar** contatainers which have discreet functionality to work properly

## K8s file

- each kubernetes config file creates an Object
- Object Types available with apiVersion: v1 are

  - componentStatus
  - configMap
  - Endpoints
  - Event
  - Namespace
  - Pod

broadly categorized as

- Pods
- Services
  - ClusterIP
  - NodePort
  - LoadBalancer
  - Ingress
- Deployments
- Secrets

* Object Types available with apiVersion: apps/v1 are

  - ControllerRevision
  - StatefulSet

  eval \$(minikube docker-env) # to connect local desktop's docker client to virtual machines

## minikube

- minikube is for development and is equivalent to EKS or kop cluster.
- it is a program which creates a virtual machine (called node which contains containers).
- Docker Desktop has a built in kubernetes.
- It is different from kubernetes in docker desktop in the sense that docker creates a virtual machine when it is installed with minikube it is not.

  ```
  minikube start / stop
  minikube status
  minikube dashboard
  minikube ip #ip address of the virtual machine
  ```

if need to switch to different driver then delete your cluster

```
minikube delete
```

and restart with a different driver

```
minikube start --driver=hyperkit ( or virtualbox)
```

if you need to setup ingress locally with minikube

```
minikube addons enable ingress
```

## Kubectl

- It is a program used in development env and used to interact with the node

  ```
  kubectl cluster-info
  kubectl apply -f <yaml file> # to spin the objects
  Kubectl get pods/services
  ```

- Command to Create secret to pass sensitive informataion such as password

  ```
  kubectl create secret generic pgpassword --from-literal PGPASSWORD=12345asdf
  ```

- in aws, either lauch kubectl on rancher or setup kubeconfig to work from local. Copy config from apprpriate cluster to local
- alternatively we can use following function in .zshrc to merge new files if added to a particulr folder (say, .kube/configs)

  ```
  function mergeKubeConfigs() {
  echo "merging kube ctl configs"
  for f in $(ls $HOME/.kube/configs); do
      cp $HOME/.kube/config $HOME/.kube/config.bak && KUBECONFIG=$HOME/.kube/config:$HOME/.kube/configs/$f kubectl config view --flatten >/tmp/config && mv /tmp/config $HOME/.kube/config
  done
  }

  mergeKubeConfigs
  ```

- other useful commands:
  ```
  $ kubectl get svc
  $ kubectl get deployments
  $ cp $HOME/.kube/uscald.yaml $HOME/.kube/config
  $ kubectl config current-context
  $ kubectl config get-contexts
  ```

## Create a KOP cluster (EKS is native to aws and can also be used instead of creating own cluster)

```
$ export KOPS_STATE_STORE=s3://clusters.k8s.appychip.vpc.us-west-1
$ export AWS_ACCESS_KEY_ID=
$ export AWS_SECRET_ACCESS_KEY=

$ kops create cluster \
--cloud=aws \
--zones=us-west-1a \
--name=uswest1.k8s.appychip.vpc \
--dns-zone=appychip.vpc \
--dns private
```
