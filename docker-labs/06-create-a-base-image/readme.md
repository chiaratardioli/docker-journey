# Lab 06 — Create a Base Image

## Objective

I learnt how to create a base image by saving changes made inside a container, then use it to build a simple application image.

## What I Practiced

* Started an Ubuntu container.
* Installed Node.js inside the container.
* Created a base image using `docker container commit`.
* Inspected image layers with `docker image history`.
* Created a simple Node.js application.
* Created an application image from the container.
* Set a default command for the application image.

## Steps

### 1. Create the base image

I started an Ubuntu container:

```bash
chiara$ docker run --name=base-container -ti ubuntu
```

Inside the container, I installed Node.js:

```bash
root@a101e676bd75:/# apt update && apt install -y nodejs
Get:1 http://ports.ubuntu.com/ubuntu-ports resolute InRelease [136 kB]
Get:2 http://ports.ubuntu.com/ubuntu-ports resolute-updates InRelease [137 kB]
Get:3 http://ports.ubuntu.com/ubuntu-ports resolute-backports InRelease [137 kB]
Get:4 http://ports.ubuntu.com/ubuntu-ports resolute-security InRelease [137 kB]
Get:5 http://ports.ubuntu.com/ubuntu-ports resolute/restricted arm64 Packages [231 kB]
Get:6 http://ports.ubuntu.com/ubuntu-ports resolute/multiverse arm64 Packages [298 kB]
Get:7 http://ports.ubuntu.com/ubuntu-ports resolute/universe arm64 Packages [19.9 MB]
Get:8 http://ports.ubuntu.com/ubuntu-ports resolute/main arm64 Packages [1860 kB]
Get:9 http://ports.ubuntu.com/ubuntu-ports resolute-updates/restricted arm64 Packages [662 kB]
Get:10 http://ports.ubuntu.com/ubuntu-ports resolute-updates/main arm64 Packages [755 kB]
Get:11 http://ports.ubuntu.com/ubuntu-ports resolute-updates/universe arm64 Packages [329 kB]
Get:12 http://ports.ubuntu.com/ubuntu-ports resolute-updates/multiverse arm64 Packages [14.3 kB]
Get:13 http://ports.ubuntu.com/ubuntu-ports resolute-backports/universe arm64 Packages [3308 B]
Get:14 http://ports.ubuntu.com/ubuntu-ports resolute-security/universe arm64 Packages [206 kB]
Get:15 http://ports.ubuntu.com/ubuntu-ports resolute-security/main arm64 Packages [594 kB]
Get:16 http://ports.ubuntu.com/ubuntu-ports resolute-security/multiverse arm64 Packages [11.2 kB]
Get:17 http://ports.ubuntu.com/ubuntu-ports resolute-security/restricted arm64 Packages [651 kB]
Fetched 26.1 MB in 2s (11.3 MB/s)                         
24 packages can be upgraded. Run 'apt list --upgradable' to see them.
Installing:                     
  nodejs

Installing dependencies:
  ca-certificates  libicu78       libsimdjson29  node-acorn             node-corepack   node-minimatch  node-xtend
  libada-url0-3    libllhttp9.3   libsimdutf31   node-balanced-match    node-debug      node-ms         nodejs-doc
  libbrotli1       libnghttp2-14  libsqlite3-0   node-brace-expansion   node-llhttp     node-semver     openssl
  libcares2        libnode127     libuv1t64      node-cjs-module-lexer  node-lru-cache  node-undici

Suggested packages:
  npm

Summary:
  Upgrading: 0, Installing: 28, Removing: 0, Not Upgrading: 24
  Download size: 38.7 MB
  Space needed: 146 MB / 453 GB available
...
```

I verified the installation:

```bash
root@a101e676bd75:/# node -e 'console.log("Hello world!")'
Hello world!
```

From a separate terminal on the host, I saved the container changes as a new image:

```bash
chiara$ docker container commit -m "Add node" base-container node-base
sha256:0a01c219b4289f81ed27ef290626ef6d852b543fb9c09ad106c0f9370566d788
```

I inspected the image layers:

```bash
chiara$ docker image history node-base
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
0a01c219b428   5 seconds ago   /bin/bash                                       172MB     Add node
2260313b31c8   3 weeks ago     umoci raw add-layer --image /home/buildd/roc…   12.3kB    Add rock control metadata
<missing>      3 weeks ago     umoci config --image /home/buildd/rockcraft-…   0B        Set annotations
<missing>      3 weeks ago     umoci config --image /home/buildd/rockcraft-…   0B        Set labels
<missing>      3 weeks ago     umoci config --image /home/buildd/rockcraft-…   0B        Set default PATH for bare-based rock
<missing>      3 weeks ago     umoci config --image /home/buildd/rockcraft-…   0B        Set default commands
<missing>      3 weeks ago     umoci config --image /home/buildd/rockcraft-…   0B        Set entrypoint
<missing>      3 weeks ago     umoci raw add-layer --image /home/buildd/roc…   135MB     
```

Now I tested the new image:

```bash
chiara$ docker run node-base node -e "console.log('Hello again')"
Hello again
```

Eventually, I removed the original container:

```bash
chiara$ docker rm -f base-container
base-container
```

### 2. Build the application image

I started a new container from `node-base`. Then, inside the container, I created a simple Node.js application and I run the application.

```bash
chiara$ docker rm -f base-container
base-container
chiara$ docker run --name=app-container -ti node-base
root@93e153fa4a3d:/# echo 'console.log("Hello from an app")' > app.js
root@93e153fa4a3d:/# node app.js
Hello from an app
root@93e153fa4a3d:/# 
```

From another terminal, I saved the changes as a new image and set the default command. I inspected the image layers and run the application image.

```bash
chiara$ docker container commit -c "CMD node app.js" -m "Add app" app-container sample-app
sha256:9425826f806ac97014fa2490f29ad683a838d82d48df8ac34accd75c3daddc9f
chiara$ docker image history sample-app
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
9425826f806a   5 seconds ago    /bin/bash                                       16.4kB    Add app
0a01c219b428   16 minutes ago   /bin/bash                                       172MB     Add node
2260313b31c8   3 weeks ago      umoci raw add-layer --image /home/buildd/roc…   12.3kB    Add rock control metadata
<missing>      3 weeks ago      umoci config --image /home/buildd/rockcraft-…   0B        Set annotations
<missing>      3 weeks ago      umoci config --image /home/buildd/rockcraft-…   0B        Set labels
<missing>      3 weeks ago      umoci config --image /home/buildd/rockcraft-…   0B        Set default PATH for bare-based rock
<missing>      3 weeks ago      umoci config --image /home/buildd/rockcraft-…   0B        Set default commands
<missing>      3 weeks ago      umoci config --image /home/buildd/rockcraft-…   0B        Set entrypoint
<missing>      3 weeks ago      umoci raw add-layer --image /home/buildd/roc…   135MB     
chiara$ docker run sample-app
Hello from an app
```

Eventually, I removed the application container:

```bash
chiara$ docker rm -f app-container
app-container
```

## Results

* **Base image:** Created `node-base` from Ubuntu after installing Node.js.
* **Image layers:** Used `docker image history` to inspect the layers and see the changes added to the image.
* **Application image:** Created `sample-app` by adding a simple Node.js application to the base image.
* **Default command:** Configured the image to run `node app.js` automatically.
* **Final result:** Ran `sample-app` and displayed the application greeting.

## Conclusion

This lab demonstrated how Docker images are built from layers and how a base image can be extended to create an application image. The next step is to learn how to build images using a Dockerfile, which is the more common and reproducible approach.


## What I learned

A **base image** provides a foundation for building other images. Using `docker container commit`, changes made inside a container can be saved as a new image layer. A new image can then extend that base image by adding application files and configuration, such as a default command. <Cite ref="turn0view0" />


