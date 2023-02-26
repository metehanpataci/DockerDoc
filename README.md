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
## Persisting DB

Create a volume by using the docker volume create command.

```
docker volume create todo-db
```

Stop the todo app container once again in the Dashboard (or with docker rm -f <container-id>), as it is still running without using the persistent volume.

Start the todo app container, but add the -v flag to specify a volume mount. We will use the named volume and mount it to /etc/todos, which will capture all files created at the path.

```
docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
```
Once the container starts up, open the app and add a few items to your todo list.

Items added to todo list

Remove the container for the todo app. Use the Dashboard or docker ps to get the ID and then docker rm -f <container-id> to remove it.

Start a new container using the same command from above.

Open the app. You should see your items still in your list!

Go ahead and remove the container when you're done checking out your list.

Hooray! You've now learned how to persist data!
  
Diving into our Volume
A lot of people frequently ask "Where is Docker actually storing my data when I use a named volume?" If you want to know, you can use the docker volume inspect command.

```
docker volume inspect todo-db
[
    {
        "CreatedAt": "2019-09-26T02:18:36Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```
The Mountpoint is the actual location on the disk where the data is stored. Note that on most machines, you will need to have root access to access this directory from the host. But, that's where it is!
  
Quick Volume Type Comparisons¶
Bind mounts and named volumes are the two main types of volumes that come with the Docker engine. However, additional volume drivers are available to support other use cases (SFTP, Ceph, NetApp, S3, and more).

Named Volumes	Bind Mounts
Host Location	Docker chooses	You control
Mount Example (using -v)	my-volume:/usr/local/data	/path/to/data:/usr/local/data
Populates new volume with container contents	Yes	No
Supports Volume Drivers	Yes	No


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

