# My Docker Journey

A collection of hands-on exercises to learn Docker through practical examples.

Each lab documents what I learned and the commands I used.

## List of labs

1. [Welcome to docker](./docker-labs/01-welcome-to-docker)
2. [Develop with containers](./docker-labs/02-develop-with-containers)
3. [Build and push an image on Docker Hub](./docker-labs/03-build-and-push-docker-image)


## Core Concepts

1. **Container**

A container is an isolated process that packages an application with the files and dependencies it needs to run. Unlike a virtual machine, it shares the host system’s kernel, making it lightweight and efficient. Containers help applications run consistently across different environments because they are isolated from the host and other containers.

2. **Docker Image**

A Docker image is a read-only package containing everything needed to run an application, including its code, dependencies, libraries, and configuration. Images are built in layers, which can be reused to make builds more efficient, and they serve as the foundation for creating containers. Unlike containers, images do not run by themselves; they are used to create and start containers. Images can be built from a Dockerfile, pulled from a registry such as Docker Hub, and shared with others.

3. 
