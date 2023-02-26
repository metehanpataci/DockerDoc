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



## F.A.Q

1. Error response from daemon: open \\.\pipe\docker_engine_linux: The system cannot find the file specified.

**Solution 1:** Restart docker Desktop

**Solution 2:**
```
cd "C:\Program Files\Docker\Docker"

./DockerCli.exe -SwitchLinuxEngine
```

