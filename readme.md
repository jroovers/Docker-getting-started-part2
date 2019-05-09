# Getting started with docker part 2

https://docs.docker.com/get-started/part2/

>The **Dockerfile** file tells Docker to do the following:
>
>* Use the official Python runtime as a parent image.
>* Copy the current directory (.) into the container at /app
>* Install any needed packages in requirements.txt
>* Make sure port 80 is available to the world outside the container
>* Define a simple environment variable
>* Run app.py once container launches.

## Run the app

```bash
# Build a image based on the dockerfile
docker build --tag=friendlyhello .
# Check that the image is in the local docker image registry
docker image ls
# Run it, map the container port 80 to our host 4000
docker run -p 4000:80 friendlyhello
```

or

```bash
# Run it in the background (detached mode)
docker run -d -p 4000:80 friendlyhello
```

You can now view the app in your browser at your docker-machine's ip at port 4000.
e.g. http://localhost:4000 or http://192.168.99.100:4000/

### Cleaning up

```bash
# Find the container ID of the container you started
docker container ls
# Stop it using the CONTAINER ID
docker container stop YOUR_CONTAINER_ID
```

### Tagging and publishing
```bash
# Login to docker hub first
docker login
# Tag your image friendlyhello
docker tag friendlyhello username/repo:tag
# Run docker image ls to see your new tagged image
docker image ls
# Upload it
docker push username/repo:tag
```

From now on you can run it on **any** machine:

```bash
docker run -p 4000:80 username/repo:tag
```