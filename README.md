# 🐳 Learn what matters - Docker

## Virtual Machine vs Docker

- Virtual machines package hardware, OS, and applications together.
- Docker (containers) package applications while reusing the host OS and hardware.

---

## Image vs Container
- **Image:** An image is an executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and configuration files..
- **Container:** A running instance of an image.

---

## Docker cli commands

```ruby

# Docker image commands

docker pull <image-name>:<tag> #=> pull an image
docker images #=> show all images available on the local machine
docker rmi <image-id | image-name> #=> delete an image from the local machine
docker build -t <image-name>:<tag> . #=> build an image

# Docker container commands

docker ps #=> show running containers
docker run <image-name> #=> run a container
docker run -d <image-name> #=> run a container in background
docker run -d --name <container-name> <image-name> #=> assign a name to the container
docker run -d -p <host-port>:<container-port> <image-name> #=> expose container port to host machine
docker start <container-name | container-id> #=> restart an existing container
docker stop <container-name | container-id> #=> stop a running container
docker logs <container-name> #=> view container logs
docker exec -it <container-name> <command> #=> run a command inside a running container
docker rm <container-name | container-id> #=> delete a container
docker rm -f <container-name> #=> force remove a running container

# Docker network commands



# Docker volume commands



```

--- 

## Docker network
Docker network enables containers to communicate with each other using container names through Docker’s built-in DNS, solving the problem of isolation.  

```ruby
# Communication between postgres and pgadmin containers

#=> step 1
docker network create p-network

#=> step 2
docker run -d --name postgres --network p-network postgres

#=> step 3
docker run -d --name pgadmin --network p-network -p 5050:80 dpage/pgadmin4
```
