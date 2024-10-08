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

docker exec -it <container name/id> /bin/bash

docker-compose up --build [OR docker compose up -- build]
docker-compose up -d [OR docker compose up -d]
docker-compose down [OR docker compose down]
docker-compose ps [docker compose ps]


docker compose up/down <service name>  ## if you want to bring up/down a specific service up ##
```
### real time monitoring of running instances

```
docker stats
```
### use following command to start a redis docker instance and map the port

```
docker run -d -p 6378:6379 redis
6378 - host port (meaning your local redis client will connect to this port)
6379 - contaner port
```

### or postgres on default port

```
docker run --name postgres-db -p 5432:5432 -e SERVICE_NAME=postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -d postgres:9.6-alpine
```

### Network in docker
```
docker network create myNetwork
docker network connect myNetwork web1 #will get a new ip and will be access using it. say, 172.20.0.2 
docker network connect myNetwork web2 #will get a new ip and will be access using it. say, 172.20.0.3

docker network ls
docker network inspect bridge
```
