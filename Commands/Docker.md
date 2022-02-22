### How to analyze docker container

Look at DockerFile to see services

```bash
./build-docker.sh 
```
// if there is a script to help you run docker

### building Docker Image from Dockerfile
```
docker build . -t <image name>
```

### run Docker

```
docker run <image name>
```

### list all docker image
```
docker image ls
```

### list all docker process

```
docker ps -a
```

### start a created container
```
docker start <container_name>
```

### set env file
```
--env-file .env
```

### expose port (5000 on host machine, 80 on docker)
```
-p 5000:80
```

###  deploy steps 
-> winscp to copy build 
-> use nginx to host the webpage in docker
-> use docker for reverse proxy