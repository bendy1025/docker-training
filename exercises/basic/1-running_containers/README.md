Here’s a more beginner-friendly version of your exercise, with simpler explanations, clearer step-by-step instructions, and fewer advanced details to keep it approachable.

---

# **Exercise 1: Getting Started with Docker Containers**

In this exercise, you'll learn the basics of using Docker to pull images, start containers, stop them, and remove them.

---

## **Step 1: Checking Installed Images**

Before running a container, we need an image. Docker images are like templates used to create containers.

1. Open a terminal and check what images are already on your machine by running:

   ```sh
   docker images
   ```

   If you just installed Docker, you’ll see an empty list:

   ```sh
   REPOSITORY   TAG   IMAGE ID   CREATED   SIZE
   ```

---

## **Step 2: Downloading an Image (Pulling an Image)**

Since we don’t have any images yet, let’s download one from [Docker Hub](https://hub.docker.com/), a website where Docker images are stored.

1. To download the latest version of Ubuntu, run:

   ```sh
   docker pull ubuntu
   ```

   Docker will download the image and show progress as it pulls different parts of the image.

2. Verify that the image is now available:

   ```sh
   docker images
   ```

   You should see something like this:

   ```sh
   REPOSITORY   TAG      IMAGE ID       CREATED       SIZE
   ubuntu       latest   a2bc5b5ef8b7   3 weeks ago   29MB
   ```

   🎉 **Great! You’ve downloaded your first Docker image.**

---

## **Step 2A: Build an Image (build an Image)**

Since we don’t have any images yet, let’s build one from scratch.

1. Create a Dockerfile copy and paste instruction below to build your own image:

```
# Use the offical Ubuntu image
FROM ubuntu:latest

# set env var to avoid interactive prompt during installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install curl and net-tool
RUN apt-get update && \
    apt-get install -y curl wget && \
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/*

# Set the default cmd to run a shell
CMD ["/bin/bash"]

```

   ```sh
   docker build -t ubuntu .
   ```
🎉 **Great! You’ve built your first Docker image.**

   Docker will build the image and show progress as it pulls different parts of the image.
---

## **Step 3: Running a Container**

A container is a running instance of an image.

1. Run a simple command inside an Ubuntu container:

   ```sh
   docker run ubuntu echo "Hello, Docker!"
   ```

   This command:
   - Starts a container using the `ubuntu` image.
   - Runs the `echo "Hello, Docker!"` command inside the container.
   - Prints `Hello, Docker!` in your terminal.
   - Stops the container automatically after running the command.

2. Check if any containers are running:

   ```sh
   docker ps
   ```

   You might see an empty list, because the container stopped after it printed the message.

3. To see **all** containers (including stopped ones), run:

   ```sh
   docker ps -a
   ```

   This will show the container that ran `echo "Hello, Docker!"`, but it will have an **Exited** status.

---

## **Step 4: Running an Interactive Container**

So far, we ran a quick command in a container. Now, let's start an Ubuntu container and interact with it like a normal computer.

1. Run the following command:

   ```sh
   docker run -it ubuntu bash
   ```

   - `-it` means **interactive mode**, so you can type commands.
   - `bash` starts a shell inside the container.

2. You should now see a prompt inside the container:

   ```sh
   root@b12345abc:/#
   ```

   You're now **inside the container**! Try running some Linux commands:

   ```sh
   ls   # Lists files
   pwd  # Shows the current directory
   whoami  # Shows the current user (should be "root")
   ```

3. To **exit the container**, type:

   ```sh
   exit
   ```

   This stops the container and returns you to your normal terminal.

---

## **Step 5: Running a Container in the Background**

By default, containers stop when the command inside them finishes. But sometimes, we want them to keep running.

1. Run an Ubuntu container that sleeps for 1 hour:

   ```sh
   docker run -d ubuntu sleep 3600
   ```

   - `-d` means **detached mode**, so it runs in the background.
   - `sleep 3600` makes the container do nothing for an hour.

2. Check running containers:

   ```sh
   docker ps
   ```

   You should see your container running.

---

## **Step 6: Stopping a Running Container**

If we don’t want to wait an hour, we can stop the container now.

1. Find the **CONTAINER ID** from `docker ps` and stop it:

   ```sh
   docker stop <CONTAINER ID>
   ```

   Example:

   ```sh
   docker stop a1b2c3d4e5f6
   ```

   Or you can use just the first few characters:

   ```sh
   docker stop a1b
   ```

2. Check if the container has stopped:

   ```sh
   docker ps
   ```

   It should no longer appear in the list.

---

## **Step 7: Removing Containers**

Containers don’t disappear when they stop. To clean them up:

1. See all containers (including stopped ones):

   ```sh
   docker ps -a
   ```

2. Remove a specific container:

   ```sh
   docker rm <CONTAINER ID>
   ```

3. Remove **all stopped containers** at once:

   ```sh
   docker rm $(docker ps -a -q)
   ```

---

## **Step 8: Removing Images**

Over time, you might want to delete unused images to free up space.

1. Check your images:

   ```sh
   docker images
   ```

2. Remove an image:

   ```sh
   docker rmi ubuntu
   ```

3. Remove **all images** from your system:

   ```sh
   docker rmi $(docker images -q)
   ```

---

## **Bonus: Automatically Remove Containers After Running**

By default, containers stay on your system after they stop. If you just need to run a quick command and don’t want to keep the container, use the `--rm` flag.

```sh
docker run --rm ubuntu echo "This container will delete itself!"
```

After it runs, it will **not** appear in `docker ps -a` because it was automatically removed.

---

### **🎯 Summary of What You Learned**
✅ Pulled an image from Docker Hub  
✅ Ran a simple command inside a container  
✅ Started an interactive container session  
✅ Ran a container in the background  
✅ Stopped and removed containers  
✅ Deleted images to free space  
✅ Used `--rm` for automatic cleanup  

🔹 **Next Steps:** Try running a different image, like `nginx` or `python`, and explore more Docker commands!

---

This version keeps the content beginner-friendly by removing overly technical details, reducing unnecessary outputs, and focusing on easy-to-follow steps. Let me know if you want any further refinements! 🚀
