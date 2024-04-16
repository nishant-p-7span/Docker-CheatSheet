# Docker-CheatSheet

## Docker Basic Commands:

```
docker run -it ubuntu
```
* it will run the container from ubuntu image. -it used for intereactive terminal. Here once you exit the terminal, you container will be stopped.

```
docker exec <container-name/is>
```
* It is used to re reun the container that is running before.

* to list all running containers.
```
docker container ls
```
* to list all running/stopped containers.
```
docker container la -a
```

* List all images:
```
docker image ls
```
```
docker image ls -a
```

* Create Volumes
```
docker volume create my-volume
```

* Run Container with that volume
```
docker run  -it --rm -v my-volume:/my-data ubuntu:22.04
```

* Bind Local storage to the containers
```
docker run  -it --rm -v ${PWD}/my-data:/my-data ubuntu:22.04
```
* Docker compose file run
```
docker-compose up
```

* Delete all the resource created by docker compose.
```
docker-compose down
```

* Run docker compose in background
```
docker-compose up -d
```

* Start stopped dokcer compose resource:
```
docker-compose start
```

* Run Docker compose file with custoome name
```
docker-compoose -f file.yaml up/down/start
```

* Docker network drivers
  > Bridge: by default driver, if nothing is speccified then this will be selected. It will create virtual network for container, so when we run conatainer we need to assign container port to local port.
```
docker run -it -p host:containerport image
```
  > Host: Cotainer can directly communicate with host/local commputer. No need for port mapping.
```
docker run -it --network=host image
```
  > none: Means container have no network diver and is not able to connect to the internet or other container.
* Inspect command for bridge.
```
docker network inspect bridge
```
* Create own docker network.
  > create network.
```
docker network create -d bridge hello
```
```
docker run -it --network=hello --name everything_is_awesome image
```
  > create another container in same netwrok hello. now they are able to communicate with each other.
```
ping hello
```
we just have to give name. and it will solve the request automatically.

* Caching layer:
  > all the commands contained in dockerfile are cached by docker in layers.
  > but if one of the layers data has changed, like there is change in hello.txt file then all the data in dockerfile after RUN: hello.txt, will be run again.
  > It is prefered to manage the order perfectly for faster run time.

* to copy all the files.
```
COPY . .
```
* use `.dockerignore` to exclude the folders.
  > if your .env file is not copying then remove it from the ignore file.

* change work directory.
```
WORKDIR /usr/app
```
  > now all the commands after that line will be executed in usr/app directory.

* Multi-Stage Build.
![image](https://github.com/nishant-p-7span/Docker-CheatSheet/assets/160576245/b4060c39-1e16-4a2f-b399-9e896a08c002)
