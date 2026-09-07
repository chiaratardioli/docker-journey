# Lab 04 — Search for and Download an Image

## Objective

Learn how to search for Docker images, download an image from Docker Hub, and inspect its layers.

## Commands

```bash
docker search docker/welcome-to-docker
docker pull docker/welcome-to-docker
docker image ls
docker image history docker/welcome-to-docker
```

## What I practiced

* Searching for images available on Docker Hub.
* Pulling an image to my local machine.
* Listing locally available Docker images.
* Inspecting the layers that make up a Docker image.
* Understanding that each image layer represents a set of filesystem changes.

## Results

```bash
chiara$ docker search docker/welcome-to-docker
NAME                                            DESCRIPTION                                     STARS     OFFICIAL
docker/welcome-to-docker                        Docker image for new users getting started w…   73        
docker/dockerfile                               Official Dockerfile frontend images that ena…   130       
docker/dockerfile-copy                          (deprecated)                                    1         
docker/docker-model-backend-llamacpp                                                            2         
docker/docker-mcp-cli-desktop-module                                                            0         
docker/desktop-docker-debug-service                                                             0         
docker/dockerfile-upstream                      Staging version of docker/dockerfile            12        
docker/docker-bench-security                    (deprecated) Docker Bench checks for dozens …   65        
docker/docker-desktop-scout-desktop-module                                                      0         
docker/docker-model-cli-desktop-module                                                          1         
docker/docker-desktop-dhi-desktop-module                                                        1         
docker/docker-desktop-ai-desktop-module                                                         0         
docker/aci-hostnames-sidecar                                                                    4         
docker/ucp-agent                                                                                13        
docker/gordon                                                                                   4         
docker/ucp-auth                                 Please refer to the docker/ucp image for mor…   4         
docker/ecs-searchdomain-sidecar                                                                 2         
docker/docker-desktop-sandbox-desktop-module    Module for coding agent sandboxes               0         
docker/ucp-interlock-proxy                                                                      2         
docker/whalesay                                 An image for use in the Docker demo tutorial    760       
docker/ucp-agent-win                                                                            1         
docker/docker-desktop-offload-desktop-module    Docker Offload Desktop Module                   0         
docker/docker-desktop-cli-desktop-module-test                                                   0         
docker/compose                                  Define and run multi-container applications …   208       
docker/docker-agent                                                                             0         
```

```bash
chiara$ docker pull docker/welcome-to-docker
Using default tag: latest
latest: Pulling from docker/welcome-to-docker
Digest: sha256:c4d56c24da4f009ecf8352146b43497fe78953edb4c679b841732beb97e588b0
Status: Image is up to date for docker/welcome-to-docker:latest
docker.io/docker/welcome-to-docker:latest
```

```bash
chiara$ docker image ls
                                                                                                                                                                        i Info →   U  In Use
IMAGE                                         ID             DISK USAGE   CONTENT SIZE   EXTRA
chiaratardi/getting-started-todo-app:latest   7e7a17068877       1.67GB          413MB        
docker/welcome-to-docker:latest               c4d56c24da4f       22.9MB         6.35MB    U   
getting-started-todo-app-backend:latest       37e16deb4435       1.78GB          436MB    U   
getting-started-todo-app-client:latest        7e7d4e21938e       1.85GB          447MB    U   
mysql:9.3                                     b9d8b7ec6e6a        1.2GB          268MB    U   
phpmyadmin:latest                             3a8a8d6b5289        828MB          190MB    U   
traefik:v3.6                                  31267173a15b        230MB         50.5MB    U   
```

```bash
chiara$ docker image history docker/welcome-to-docker
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
c4d56c24da4f   13 months ago   COPY /app/build /usr/share/nginx/html # buil…   1.65MB    buildkit.dockerfile.v0
<missing>      14 months ago   CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      14 months ago   STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      14 months ago   EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      14 months ago   ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      14 months ago   COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      14 months ago   COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      14 months ago   COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      14 months ago   COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      14 months ago   COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      14 months ago   RUN /bin/sh -c set -x     && addgroup -g 101…   5.63MB    buildkit.dockerfile.v0
<missing>      14 months ago   ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      14 months ago   ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      14 months ago   ENV NGINX_VERSION=1.29.0                        0B        buildkit.dockerfile.v0
<missing>      14 months ago   LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      14 months ago   CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      14 months ago   ADD alpine-minirootfs-3.22.1-aarch64.tar.gz …   9.17MB    buildkit.dockerfile.v0
```

```bash
chiara$ docker ps
CONTAINER ID   IMAGE                              COMMAND                  CREATED       STATUS                 PORTS                                 NAMES
220d51fbca3c   getting-started-todo-app-backend   "docker-entrypoint.s…"   2 hours ago   Up 2 hours                                                   getting-started-todo-app-backend-1
3ace474eb6c1   phpmyadmin                         "/docker-entrypoint.…"   2 hours ago   Up 2 hours             80/tcp                                getting-started-todo-app-phpmyadmin-1
1d20eaf62bb7   getting-started-todo-app-client    "docker-entrypoint.s…"   2 hours ago   Up 2 hours                                                   getting-started-todo-app-client-1
3a379ae7a71e   traefik:v3.6                       "/entrypoint.sh --pr…"   2 hours ago   Up 2 hours             0.0.0.0:80->80/tcp, [::]:80->80/tcp   getting-started-todo-app-proxy-1
25b56e851d59   mysql:9.3                          "docker-entrypoint.s…"   2 hours ago   Up 2 hours (healthy)   3306/tcp, 33060/tcp                   getting-started-todo-app-mysql-1
```

## What I learned

Docker images are built from multiple layers. Each layer contains filesystem changes, and Docker can reuse these layers between images, making image storage and distribution more efficient.
