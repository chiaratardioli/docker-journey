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
docker run --name=base-container -ti ubuntu
```

Inside the container, I installed Node.js:

```bash
apt update && apt install -y nodejs
```

I verified the installation:

```bash
node -e 'console.log("Hello world!")'
```

From a separate terminal on the host, I saved the container changes as a new image:

```bash
docker container commit -m "Add node" base-container node-base
```

I inspected the image layers:

```bash
docker image history node-base
```

Now I tested the new image:

```bash
docker run node-base node -e "console.log('Hello again')"
```

Eventually, I removed the original container:

```bash
docker rm -f base-container
```

### 2. Build the application image

I started a new container from `node-base`:

```bash
docker run --name=app-container -ti node-base
```

Inside the container, I created a simple Node.js application:

```bash
echo 'console.log("Hello from an app")' > app.js
```

I run the application:

```bash
node app.js
```

From the host terminal, I saved the changes as a new image and set the default command:

```bash
docker container commit -c "CMD node app.js" -m "Add app" app-container sample-app
```

I inspected the image layers:

```bash
docker image history sample-app
```

I run the application image:

```bash
docker run sample-app
```

Eventually, I removed the application container:

```bash
docker rm -f app-container
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


