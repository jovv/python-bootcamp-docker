# Solution

Create a Dockerfile and build the image.
```cmd
cd exercises/exercise3
docker build -t exec3 .
```

Run a container using the image.
```cmd
docker run exec3
```

Show all containers (including stopped ones),
to get the container id.
```cmd
docker ps -al
```

Show the logs for the container.
```cmd
docker logs <container-id>
```