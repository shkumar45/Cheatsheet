## Docker Commands

```
docker container ls
docker container kill <container id>
docker build [-f Dockerfile.dev] .
docker build -t skumar/<tag> . # Builds an image using Dockerfile in current directory and tags it

docker push shkumar45/multi-client:tagname

docker run <image id>
docker run -it alpine sh    # get a shell
docker ps
docker commit -c 'CMD ["redis-server"]' <cd269634eed9>
docker run -p 8081:8080 skumar/simpleweb

docker-compose up --build
docker-compose up -d
docker-compose down
docker-compose ps
```


### use following command to start a redis docker instance and map the port
```
docker run -d -p 6378:6379 redis
6378 - host port (meaning your local redis client will connect to this port)
6379 - contaner port
```

## minikube

- minikube is for development and is equivalent to EKS or kubernetes.
- it is a program which creates a virtual machine (called node which contains containers).
- Docker Desktop has a built in kubernetes.
- It is different from kubernetes in docker desktop in the sense that docker creates a virtual machine when it is installed with minikube it is not.

```
minikube start / stop
minikube status
minikube dashboard
minikube ip #ip address of the virtual machine
```

## Kubectl

It is a program used in development env and used to interact with the node

```
kubectl cluster-info
kubectl apply -f <yaml file> # to spin the objects
Kubectl get pods/services
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
- Deployments

* Object Types available with apiVersion: apps/v1 are

  - ControllerRevision
  - StatefulSet

  eval \$(minikube docker-env) # to connect local desktop's docker client to virtual machines
