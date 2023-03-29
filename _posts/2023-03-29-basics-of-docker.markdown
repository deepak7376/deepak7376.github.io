
### 1. Docker Image
Docker image is onion like layer which is build by docker build command. There are two method to create docker image
- pull the image from the docker hub
```bash
docker pull ubuntu:latest
```
- create your own image via Dockerfile
```dockerfile
# syntax=docker/dockerfile:1
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```
- If you creating image via dockerfile the you to build it first
```bash
# ex: docker build -t <Image-name> <Dockerfile path>
docker build -t getting-started .
```
- Check all docker images available
```bash
docker images
```

- Remove images
```bash
docker rmi <image id>
```
- Remove dangling images
```bash
docker images -qf "dangling=true" (its check the dangling image)
docker rmi $(docker images -qf "dangling=true")
```
### 2. Run Docker Image inside a container
Now we have docker image now run it inside the container.
syntax for docker run
```
docker run -it -d ubuntu
  --detach (-d) detach run in background, 
 --attach(-a) attach, 
 --name : assign name to container
 --volume (-v) : bind mount a volume, 
 --workdir (-w) : working directory inside container
 ```
```bash
ex: docker run -it <image>
ex: docker exec -it <CID> execute the cmd inside docker
docker run -d -t –name myubuntu ubuntu

```

### 3.Execute command inside docker
```bash
ex: docker exec -it <CONTAINER ID>
docker exec -it myubuntu bash   bash or sh
```
### 4. Stop the container
```bash
docker stop <CONTAINER ID>
docker start <CONTAINER ID> 
```
### 5. Commit the container
```bash
docker commit <CONTAINER ID> deepak/ubuntu
```
### 6. Push container to docker hub
```bash
docker push deepak/ubuntu : push to docker-hub 
```

### 7. Remove container
```bash
docker rm <CONTAINER ID>
```
### 8. Delete all obsolete Docker images with prune
```bash
# First delete all stopped containers
docker container prune
# Then delete both dangling and unused images
docker image prune --all
```
### 9. Check the status of running container
```bash
docker ps -a (all container)
docker ps (only running container)
```

### 10. Example of docker run command (advance)
```bash
docker run -it --name <CONTAINER NAME> -p 8888:8888 --volume c:/Data:/Data --workdir /Data/ <IMAGE NAME> bash
```
Mount volume
```bash
docker run -v /does not/exist:/foo -w /foo -i -t ubuntu bash
```
Note: for windows use full path with forward slash (/) not backward
Note: When the host directory of a bind-mounted volume doesn’t exist, Docker will automatically create this directory on the host for you. In the example above, Docker will create the ```/does not/exist``` folder before starting your container.

Attach multiple volume in container
```bash
docker run --name linuxMachine -p 8000:8000 -v c:/eSensor/hdd1:/hdd1 -v c:/eSensor/hdd2:/hdd2 -i -t ubuntu:18.04 bash
```

Use this most of time (Default container creation setting)
```bash
docker run -it --name tf-models --gpus all --network host  -v /home/deepak/Task/models:/home/models -w /home/models tensorflow/tensorflow bash
```

### 11. Docker compose 
Docker compose is basically combination of = docker build + docker run command
```bash
docker build -t <IMAGE_NAME> <DIR_NAME>  ( it create image from docker file)
docker run –rm -p 3000:3000 -n <CONTAINER NAME> -i -t <IMAGE_NAME> bash (it run the container)
```
```bash
Docker-compose up -d (creating image using docker file) 
```


