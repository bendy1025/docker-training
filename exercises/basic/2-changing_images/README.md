---

# **Exercise 2: Modifying a Docker Image**

In this exercise, you'll learn how to modify an existing Docker image and save it as a new image. We'll use the `ubuntu` image and add the `ping` command to it.

---

## **Step 1: Downloading the Ubuntu Image**
First, make sure you have the Ubuntu 16.04 image. If you completed Exercise 1, you might already have it.

1. Pull the Ubuntu image from Docker Hub:

   ```sh
   docker pull ubuntu:16.04
   ```

2. Check that the image is available on your machine:

   ```sh
   docker images
   ```

   You should see something like this:

   ```sh
   REPOSITORY   TAG      IMAGE ID       CREATED       SIZE
   ubuntu       16.04    6a2f32de169d   4 weeks ago   117MB
   ```

---

## **Step 2: Running a Container from the Image**
Now, let’s start a container using this image so we can modify it.

1. Run an interactive Ubuntu container:

   ```sh
   docker run -it ubuntu:16.04 bash
   ```

   You'll see a prompt inside the container, meaning you're inside a running Ubuntu environment:

   ```sh
   root@123456789abc:/#
   ```

2. Try running the `ping` command:

   ```sh
   ping google.com
   ```

   You'll likely see an error:

   ```sh
   bash: ping: command not found
   ```

   This is because the default Ubuntu Docker image is minimal and does not include `ping`.

---

## **Step 3: Installing the Ping Utility**
Since `ping` is missing, let's install it.

1. First, update the list of available software:

   ```sh
   apt-get update
   ```

   This downloads a list of available software packages so we can install new tools.

2. Now, install the `ping` command:

   ```sh
   apt-get install -y iputils-ping
   ```

   The `-y` flag tells Ubuntu to automatically confirm the installation.

3. Verify that `ping` is installed:

   ```sh
   ping -c 3 google.com
   ```

   If successful, you'll see output like this:

   ```sh
   PING google.com (142.250.64.142) 56(84) bytes of data.
   64 bytes from google.com: icmp_seq=1 ttl=118 time=10 ms
   64 bytes from google.com: icmp_seq=2 ttl=118 time=9 ms
   64 bytes from google.com: icmp_seq=3 ttl=118 time=9 ms

   --- google.com ping statistics ---
   3 packets transmitted, 3 received, 0% packet loss, time 2034ms
   ```

4. Exit the container:

   ```sh
   exit
   ```

---

## **Step 4: Creating a New Image**
Now that we have modified the container by installing `ping`, we can save this container as a new image so we don’t have to reinstall `ping` every time.

1. Find the **container ID** of the stopped container:

   ```sh
   docker ps -a
   ```

   You'll see a list of containers, and one will have an **Exited** status. Note its **CONTAINER ID**:

   ```sh
   CONTAINER ID   IMAGE         COMMAND       STATUS      NAMES
   123456789abc   ubuntu:16.04  "/bin/bash"   Exited     cool_container
   ```

2. Use `docker commit` to save this container as a new image:

   ```sh
   docker commit -a "Your Name" -m "Added ping command" 123456789abc myubuntu:ping
   ```

   - Replace `123456789abc` with your actual **CONTAINER ID**.
   - `myubuntu:ping` is the name of the new image.
   - `-a "Your Name"` adds your name as the author.
   - `-m "Added ping command"` is a short message describing the change.

3. Verify the new image:

   ```sh
   docker images
   ```

   You should see your new image listed:

   ```sh
   REPOSITORY       TAG     IMAGE ID       CREATED         SIZE
   myubuntu         ping    9f8a0d3b6c4e   1 minute ago    159MB
   ubuntu           16.04   6a2f32de169d   4 weeks ago     117MB
   ```

---

## **Step 5: Running a Container from the New Image**
Now that we have our new image (`myubuntu:ping`), let's test it.

1. Run a new container from this image:

   ```sh
   docker run -it myubuntu:ping bash
   ```

2. Once inside the container, test if `ping` is available:

   ```sh
   ping -c 3 google.com
   ```

   If the command works, it means your modified image was created successfully! 🎉

---

## **Summary**
✅ Pulled an image from Docker Hub  
✅ Started a container and installed new software (`ping`)  
✅ Saved the modified container as a new image  
✅ Created a new container from the modified image  

Now, every time you use `myubuntu:ping`, it will have `ping` pre-installed! 🚀

Would you like to learn how to create a Dockerfile next? That’s an even better way to build custom images! 😊
