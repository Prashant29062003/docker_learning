Notes:
1. [[Docker Container]]
2. [[Docker Images]]
3. [[Docker files]]

*best path to check docker commands use `docker` in terminal.*
## 🏗️ 1. [[Image Management]]

Images are the "blueprints" for your containers.

- **`docker pull <image_name>`**: Downloads an image from Docker Hub to your local machine.
    
- **`docker images`**: Lists all locally stored images, including their IDs and sizes.
    
- **`docker rmi <image_id>`**: Removes a specific image.
    
    - _Note: You cannot remove an image if a container (even a stopped one) is still using it._
        

---

## 🚀 2. [[Starting & Running Containers]]

This is where the magic happens.

- **`docker run <image_name>`**: Creates and starts a container from an image.
    
- **`docker run -d <image_name>`**: **Detached Mode.** Runs the container in the background, giving you your terminal back immediately.
    
- **`docker run --name <custom_name> <image_name>`**: Assigns a friendly name to your container so you don't have to copy-paste long IDs.
    

---

## 🔍 3. Monitoring & Inspection

Checking the "health" and status of your environment.

- **`docker ps`**: Shows only **running** containers.
    
- **`docker ps -a`**: Shows **all** containers (Running, Exited, or Stopped).
    
- **`docker logs <container_id>`**: (Useful Add) Shows the output/errors of a container running in detached mode.
    

---

## 🛠️ 4. Interaction & Execution

Going inside the "box" to see what's happening.

- **`docker exec -it <container_id> /bin/bash`**: Opens an interactive terminal inside a running container.
    
    - `-i`: Interactive.
        
    - `-t`: Terminal (TTY).
        
    - _Note: If `/bin/bash` doesn't work (common in Alpine Linux), try `/bin/sh`._
        

---

## 🛑 5. Stopping & Cleanup

Keeping your system lean.

- **`docker stop <container_id>`**: Gracefully shuts down a running container.
    
- **`docker rm <container_id>`**: Deletes a **stopped** container.
    
- **`docker rm -f <container_id>`**: Forces the removal of a container even if it's currently running.
    
- **`docker container prune`**: (Useful Add) Deletes **all** stopped containers at once.
    

---

### Summary Table: `rm` vs `rmi`

|**Command**|**Full Name**|**Target**|
|---|---|---|
|**`rm`**|remove|**Containers** (Instances)|
|**`rmi`**|remove image|**Images** (Blueprints)|
