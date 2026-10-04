Skip typing -n chatbot: make it your default namespace.
```kubectl config set-context --current --namespace=chatbot
kubectl config view --minify | grep namespace     # confirm
```

# Overview

```kubectl -n chatbot get all                        # pods, deployments, replicasets, services
kubectl -n chatbot get pods -o wide               # + pod IP and node
kubectl -n chatbot get pods -w                    # watch status changes live
kubectl -n chatbot get svc,pvc,secret,configmap   # everything else we created
kubectl get ns                                    # all namespaces
kubectl get pv                                    # volumes backing the PVC
```
# Logs

```kubectl -n chatbot logs deploy/api                # current logs
kubectl -n chatbot logs deploy/api -f             # follow (Ctrl+C to stop)
kubectl -n chatbot logs deploy/api --tail 50      # last 50 lines
kubectl -n chatbot logs deploy/api --since 10m    # last 10 minutes
kubectl -n chatbot logs deploy/api --previous     # the crashed container's logs (after a restart)
kubectl -n chatbot logs -l app=ui -f              # by label
```
# Debugging

```kubectl -n chatbot describe pod -l app=api        # events: image pulls, probe failures, OOMKilled
kubectl -n chatbot describe deploy/api
kubectl -n chatbot get events --sort-by=.lastTimestamp   # recent cluster events
kubectl -n chatbot get pod -l app=api -o yaml     # the full live spec
kubectl top pods -n chatbot                       # CPU/memory (needs: minikube addons enable metrics-server)
```
# Inside the containers
```
kubectl -n chatbot exec -it deploy/api -- sh      # shell into the API container
kubectl -n chatbot exec deploy/api -- env | sort  # check env vars from ConfigMap/Secret
kubectl -n chatbot exec deploy/api -- ls -la /data            # SQLite volume contents
kubectl -n chatbot exec deploy/ui -- python -c "import httpx; print(httpx.get('http://api:8000/health').text)"
kubectl -n chatbot run tmp --rm -it --image=curlimages/curl -- curl -s http://api:8000/health   # throwaway test pod
```
# Access from your Mac
```
kubectl -n chatbot port-forward svc/ui 3000:3000  # UI  → http://localhost:3000
kubectl -n chatbot port-forward svc/api 8000:8000 # API → http://localhost:8000/health
minikube service ui -n chatbot                    # NodePort via minikube tunnel
```
# Restarts and rollouts
```
kubectl -n chatbot rollout restart deploy/api     # restart (e.g. after re-loading :latest)
kubectl -n chatbot rollout status deploy/api      # wait for the rollout to finish
kubectl -n chatbot rollout history deploy/api
kubectl -n chatbot rollout undo deploy/api        # roll back to the previous version
kubectl -n chatbot delete pod -l app=api          # kill the pod; the Deployment recreates it
```
Terraform owns these resources, so changes like scale or set image made with kubectl will b next terraform apply. Make lasting changes in the .tf files, and use kubectl for looking,debugging and restarting.

# Config and secrets
```
kubectl -n chatbot get configmap chatbot-api-config -o yaml
kubectl -n chatbot describe secret chatbot-api-keys            # key names + sizes only
kubectl -n chatbot get secret chatbot-api-keys -o jsonpath='{.data.OPENAI_API_KEY}' | base64 -d | head -c 8; echo   # first 8 chars
```
After changing a ConfigMap or Secret, the pods don't pick up the new values until they resty/api.

# Minikube helpers
```
minikube status
minikube image ls | grep langgraph                # images available to the cluster
minikube image load skumar45/langgraph-chatbot-backend:latest
minikube dashboard                                # web UI for the cluster
minikube addons enable metrics-server             # enables `kubectl top`
```
# Cleanup

Prefer Terraform here, since it created these resources:
```
terraform -chdir=terraform destroy                # removes everything, including the PVC data
kubectl delete namespace chatbot                  # kubectl equivalent; leaves Terraform st
minikube stop                                     # pause the cluster
minikube delete
```



---
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
- useful read - Goodbye Docker Desktop, Hello Minikube! [link](https://itnext.io/goodbye-docker-desktop-hello-minikube-3649f2a1c469)
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
