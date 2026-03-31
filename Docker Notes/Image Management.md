Images are the "blueprints" for your containers.

- **`Downloads an image from Docker Hub to your local machine.`**
```
  docker pull <image_name>
```
    
- **`Lists all locally stored images, including their IDs and sizes.`**
```
docker images
```
    
- **`Removes a specific image.`**
```
docker rmi <image_id> 
```
    
    - _Note: You cannot remove an image if a container (even a stopped one) is still using it.
---
