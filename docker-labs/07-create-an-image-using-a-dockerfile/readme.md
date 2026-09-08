# Lab 07 — Create an Image Using a Dockerfile

## Objective

Learn how to create a Docker image using a Dockerfile and use it to run a simple Node.js application.

## What I Practiced

* Identified the main Dockerfile instructions.
* Created a Dockerfile from scratch.
* Selected a base image.
* Set the working directory.
* Copied application files into the image.
* Installed application dependencies.
* Configured the default startup command.

## Steps

### 1. Prepare the project

I cloned the `https://github.com/docker/getting-started-todo-app` project repository and switch to the `build-image-from-scratch` branch.

Since I want to create a new `Dockerfile`, I delete the existing one located in the folder `getting-started-todo-app/app/`.


### 2. Create the Dockerfile

I created a new file named `Dockerfile` inside the `app` folder. The file must not have an extension.
I added the following instructions:

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY . .

RUN yarn install --production

CMD ["node", "./src/index.js"]
```

### 3. Understand the instructions

* `FROM node:22-alpine` selects the base image.
* `WORKDIR /app` sets the working directory inside the image.
* `COPY . .` copies the project files into the image.
* `RUN yarn install --production` installs the application dependencies.
* `CMD ["node", "./src/index.js"]` sets the default command used to start the application.

### 4. Build the image

I run the following command from the project’s `app` directory:

```bash
docker build -t getting-started .
```

The `-t` option gives the image the name `getting-started`.

The final `.` tells Docker to use the current directory as the build context.

### 5. Run the application

I started a container from the new image:

```bash
docker run -p 3000:3000 getting-started
```

The application should now be available at:

```text
http://localhost:3000
```

## Results

* **Dockerfile:** Created a Dockerfile from scratch.
* **Base image:** Used `node:22-alpine`.
* **Application files:** Copied the project files into the image.
* **Dependencies:** Installed the required packages with Yarn.
* **Default command:** Configured the image to run `node ./src/index.js`.
* **Final result:** Built the image and started the Node.js application in a container.

## Conclusion

This lab demonstrated how a Dockerfile defines the steps used to build an image. The main instructions specify the base image, working directory, application files, dependencies, and startup command. Dockerfiles provide a more reproducible approach to image creation than manually using `docker container commit`.
