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
