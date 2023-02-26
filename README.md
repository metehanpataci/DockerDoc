# DockerDoc
Docker commands and notes

## DockerFile
```
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```
```
docker build -t getting-started .
```

## RUN
docker run -d -p 80:80 docker/getting-started

## Removing a container using the CLI
Get the ID of the container by using the docker ps command.

```
docker ps
```
Use the docker stop command to stop the container.


Swap out <the-container-id> with the ID from docker ps
```
docker stop <the-container-id>
```
Once the container has stopped, you can remove it by using the docker rm command.

```
docker rm <the-container-id>
```

## F.A.Q

1. Error response from daemon: open \\.\pipe\docker_engine_linux: The system cannot find the file specified.

**Solution 1:** Restart docker Desktop

**Solution 2:**
```
cd "C:\Program Files\Docker\Docker"

./DockerCli.exe -SwitchLinuxEngine
```

