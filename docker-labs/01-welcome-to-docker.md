# Lab 01 — Welcome to Docker

## Objective

Run a Docker container and access a web application from my local machine.

## Command

```bash
docker run -d -p 8080:80 docker/welcome-to-docker
```

## Result

The container started successfully and the application was accessible at:

http://localhost:8080

![Welcome to Docker](./images/01-welcome-to-docker.png)

## What I learned

* A container runs an application in an isolated environment.
* Docker can download an image if it is not available locally.
* Port mapping makes a containerized web application accessible from my computer.
* `docker ps` shows running containers.
* `docker stop` stops a running container.

## Next step

Continue the official Docker Get Started tutorial and learn how to build and run my own containerized application.
