# My Docker Journey

A collection of hands-on exercises to learn Docker through practical examples.

Each lab documents what I learned and the commands I used.

## List of Labs

1. [Welcome to docker](./docker-labs/01-welcome-to-docker)
2. [Develop with containers](./docker-labs/02-develop-with-containers)
3. [Build and push an image on Docker Hub](./docker-labs/03-build-and-push-docker-image)
4. [Search and download an image](./docker-labs/04-search-and-download-image)
5. [Docker Compose](./docker-labs/05-docker-compose)


## Core Concepts

1. **Container**

A container is an isolated process that packages an application with the files and dependencies it needs to run. Unlike a virtual machine, it shares the host system’s kernel, making it lightweight and efficient. Containers help applications run consistently across different environments because they are isolated from the host and other containers.

2. **Docker Image**

A Docker image is a read-only package containing everything needed to run an application, including its code, dependencies, libraries, and configuration. Images are built in layers, which can be reused to make builds more efficient, and they serve as the foundation for creating containers. Unlike containers, images do not run by themselves; they are used to create and start containers. Images can be built from a Dockerfile, pulled from a registry such as Docker Hub, and shared with others.

3. **Docker Registry**

An image registry is a centralized location for storing and sharing your container images. It can be either public or private. Docker Hub is a public registry that anyone can use and is the default registry. Other available image registries include Amazon Elastic Container Registry (ECR), Azure Container Registry (ACR), and Google Container Registry (GCR). It is also possible to run a private registry on your local system or inside your organization, using solutions such as Harbor, JFrog Artifactory, or GitLab Container Registry. A registry contains repositories, and each repository can contain multiple versions of an image identified by tags. This allows developers to build an image once, push it to a registry, and then pull and run it on another machine or environment.

4. **Docker Composer**

Docker Compose allows applications composed of multiple containers, such as web applications, databases, and caches, to be defined and run together. Instead of managing each container separately with multiple `docker run` commands, the configuration is described in a single YAML file. Compose is a declarative tool: the file describes the desired state of the application, and `docker compose up` creates or updates the containers to match it. A Dockerfile defines how to build an image, while a Compose file defines how to configure and run the containers.

5. **Image Layers**

Docker images are composed of immutable layers, where each layer contains a set of filesystem changes, such as adding, deleting, or modifying files. For example, an image might include a base operating system, a Python runtime, application dependencies, and the application source code, each added in a separate layer. These layers can be reused between images, making builds faster and reducing storage and bandwidth usage. When a container starts, Docker stacks the image layers into a unified filesystem and adds a separate writable layer for the container’s changes, leaving the original image layers untouched. This allows multiple containers to run from the same image while maintaining their own filesystem changes.

6. 
