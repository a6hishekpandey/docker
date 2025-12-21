# Learn what matters - Docker

## Virtual Machine vs Docker

- **Virtual Machine:** Virtual machines package hardware, OS, and applications together.
- **Docker:** Docker (containers) package applications while reusing the host OS and hardware.

---

## Image vs Container
- **Image:** An image is an executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and configuration files..
- **Container:** A running instance of an image.

---

## Docker cli commands

```ruby
# Docker image commands

docker pull <image-name>:<tag>       #=> pull an image
docker images                        #=> show all images available on the local machine
docker rmi <image-id | image-name>   #=> delete an image from the local machine
docker build -t <image-name>:<tag> . #=> build an image

# Docker container commands

docker ps                                                  #=> show running containers
docker run <image-name>                                    #=> run a container
docker run -d <image-name>                                 #=> run a container in background
docker run -d --name <container-name> <image-name>         #=> assign a name to the container
docker run -d -p <host-port>:<container-port> <image-name> #=> expose container port to host machine
docker start <container-name | container-id>               #=> restart an existing container
docker stop <container-name | container-id>                #=> stop a running container
docker logs <container-name>                               #=> view container logs
docker exec -it <container-name> <command>                 #=> run a command inside a running container
docker rm <container-name | container-id>                  #=> delete a container
docker rm -f <container-name>                              #=> force remove a running container

# Docker network commands

docker network ls                    #=> lists all available docker networks
docker network create <network-name> #=> create a docker network
docker network rm <network-name>     #=> delete a docker network
docker network prune                 #=> deletes all unused docker networks
 
# Docker volume commands

docker volume ls                   #=> lists all available docker volumes
docker volume create <volume-name> #=> create a docker volume
docker volume rm <volume-name>     #=> delete a docker volume
docker volume prune                #=> deletes all unused docker volumes
```

--- 

## Docker network
Docker network enables containers to communicate with each other using container names through Docker’s built-in DNS, solving the problem of isolation.  

```ruby
# step 1
docker network create <network-name>

# step 2
docker run -dit -p <host-port>:<container-port> -e POSTGRES_PASSWORD=<password> -e POSTGRES_USER=<user> -e POSTGRES_DB=<db> --name <container-name> --network <network-name> <image-id>

# step 3
docker run -dit -p <host-port>:<container-port> -e PGADIM_DEFAULT_EMAIL=<email> -e PGADIM_DEFAULT_PASSWORD=<password> --name <container-name> --network <network-name> <image-id>
```

---

## Docker volume
Docker volume is a persistent storage mechanism that stores data outside the container lifecycle, ensuring data is not lost when containers stop or are removed.  

```ruby
# step 1
docker volume create <volume-name>

# step 2
docker run -dit -p <host-port>:<container-port> -e POSTGRES_PASSWORD=<password> -e POSTGRES_USER=<user> -e POSTGRES_DB=<db> --name <container-name> --network <network-name> -v <volume-name>:/var/lib/postgresql/data <image-id>
```

---

## Docker compose
Docker compose is a tool used to define and run multi-container Docker applications using a single YAML configuration file.  

- docker.yml
```yml
version: "3.9"

services:
  service-name:
    image: image-name
    ports:
      - "host-port:container-port"
    environment:
      key: value
    depends_on: second-service-name

  second-service-name:
    image: image-name
    ports:
      - "host-port:container-port"
    environment:
      key: value
    volumes:
      - volume-name:path

volumes:
  volume-name:
    external: true

networks:
  network-name:
```

- commands to start/stop containers defined in docker.yml file
```ruby
docker compose -f docker.yml up #=> spin-up containers
docker compose down             #=> tear-down containers
```
