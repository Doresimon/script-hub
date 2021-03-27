# docker

## install on ubuntu

```bash
# remove old packages
sudo apt remove docker docker-engine docker.io containerd runc
# Update the apt package index and install packages to allow apt to use a repository over HTTPS:
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
# Add Docker’s official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
# Use the following command to set up the stable repository.
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# install
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## commands

### quick commands

```bash
# !
docker ps -a

## image
# list images
docker images

## container
# list containers
docker container ls -a
# Remove all stopped containers
docker container prune

## exec
# docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
docker exec

## run
# docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
docker run

## kill
# docker kill [OPTIONS] CONTAINER [CONTAINER...]
docker kill
```

### docker run

```bash
# docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
# Options:
#    -d, --detach                         Run container in background and print container ID
#    -p, --publish list                   Publish a container's port(s) to the host

sudo docker run hello-world

sudo docker run -d -p 80:80 hello-world
```

### docker exec

```bash
# docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
# Options:
#    -i, --interactive          Keep STDIN open even if not attached

export CONTAINER_ID=a7c07d0425e2d919c6632c55e268e93d354a078b09f1ac5c41447da1bed4bdf9
sudo docker exec -it $CONTAINER_ID /bin/sh
sudo docker exec -it $CONTAINER_ID /bin/bash

sudo docker run -d -p 80:80 hello-world
```
