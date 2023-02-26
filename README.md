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

## Create Repo

docker push YOUR-USER-NAME/getting-started

### Pushing our Image
In the command line, try running the push command you see on Docker Hub. Note that your command will be using your namespace, not "docker".

```
$ docker push docker/getting-started
```

The push refers to repository [docker.io/docker/getting-started]
An image does not exist locally with the tag: docker/getting-started
Why did it fail? The push command was looking for an image named docker/getting-started, but didn't find one. If you run docker image ls, you won't see one either.

To fix this, we need to "tag" our existing image we've built to give it another name.

Login to Docker Hub by either clicking on the "Sign In" button in Docker Desktop or using the command docker login -u YOUR-USER-NAME.

Use the docker tag command to give the getting-started image a new name. Be sure to swap out YOUR-USER-NAME with your Docker ID.

```
docker tag getting-started YOUR-USER-NAME/getting-started
```

Now try your push command again. If you're copying the value from Docker Hub, you can drop the tagname portion, as we didn't add a tag to the image name. If you don't specify a tag, Docker will use a tag called latest.

```
docker push YOUR-USER-NAME/getting-started
```


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

