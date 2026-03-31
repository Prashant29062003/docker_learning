This is the "Running & Managing" phase of the Docker lifecycle. Professional notes should categorize these by **Action**, **Interaction**, and **Bulk Management** to make them a quick-reference guide for a developer.

---

## 🚀 1. The `docker run` Lifecycle

The `run` command is actually a combination of `docker create` and `docker start`. It transforms an image into a live container.

- **Standard Run:** `docker run <image_name>`
    
    _Starts the container and attaches your terminal to the process._
    
- **Detached Mode (`-d`):** `docker run -d <image_name>`
    
    _Runs the container in the background. Use this for servers or databases._
    
- **Custom Naming (`--name`):** `docker run --name my-web-app <image_name>`
    
    _Replaces the random "funny_einstein" names with something readable._
    
- **Port Mapping (`-p`):** `docker run -p 8080:80 <image_name>`
    
    _Connects your machine's port to the container's port. `[Host]:[Container]`._
    
- **Volume Mounting (`-v`):** `docker run -v $(pwd):/app <image_name>`
    
    _Syncs your current folder to the `/app` folder inside the container. Essential for Hot-Reloading._
    
- **Interactive Shell (`-it`):** `docker run -it <image_name> /bin/bash`
    
    _Drops you directly into the container's terminal._
    

---

## 🔍 2. Monitoring & Inspection

Commands to see what is happening under the hood.

- **Active Containers:** `docker ps`
    
    _Shows only running containers._
    
- **Complete History:** `docker ps -a`
    
    _Shows all containers, including those that crashed or exited._
    
- **Logging:** `docker logs <container_name>`
    
    _Displays the console output (stdout) of a container. Vital for debugging detached containers._
    
- **Re-attaching:** `docker attach <container_name>`
    
    _Re-connects your terminal to a container running in the background._
    

---

## 🛑 3. Termination & Cleanup

How to stop and remove instances.

- **Graceful Stop:** `docker stop <container_id>`
    
    _Sends a `SIGTERM` signal, giving the app time to save data and shut down properly._
    
- **Hard Kill:** `docker kill <container_id>`
    
    _Sends a `SIGKILL` signal. Immediate shutdown—use only if `stop` fails._
    
- **Bulk Stop:** `docker stop $(docker ps -q)`
    
    _The `-q` flag returns only the IDs. This command feeds those IDs into `stop` to shut everything down at once._
    
- **remove permanently:** `docker rm <container_id>`
    
    _Sends a `remove` signal._
    
- **remove permanently forcefully:** `docker rm -f <container_id>`
    
    _`remove` the container forcefully _
    
- **Prune Container:** `docker <container_name> prune`
    
    _removes the non running containers._
    
- **copy container:** `docker cp <container_name>:/path/to/file ./`
    
    _copies the container form dedicated path to dedicated path like(`./` ---> current directory)_
    
---

### 💡 Professional Example Scenario

Imagine you are developing a **Node.js** app and want to run it in the background with a specific name, accessible on port 3000, while syncing your code:

Bash

```
# 1. Start the container professionally
docker run -d \
  --name my-dev-server \
  -p 3000:3000 \
  -v $(pwd):/app \
  node-app-image

# 2. Check if it's running
docker ps

# 3. Check the startup logs to ensure no errors
docker logs my-dev-server

# 4. If you need to fix something inside the container
docker exec -it my-dev-server sh

# 5. Finished? Stop everything
docker stop my-dev-server
```

### ⚠️ Note on `docker kill` vs `docker rm`

In your initial notes, you mentioned `docker kill` deletes the container. Just a small correction: **`kill` stops the process immediately, but the container still exists (in a "Exited" state).** To actually delete the container and free up disk space, you must use **`docker rm <container_name>`**.