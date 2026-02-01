# Experiment 2 – Docker Installation, Configuration, and Running Images

## Aim
To install Docker on macOS, pull images, run containers, and manage the container lifecycle, demonstrating containerization concepts.

---

#!/bin/bash

# Step 1: Pull the latest Nginx image
docker pull nginx

# Step 2: Run a container in detached mode with port mapping 8080:80
container_id=$(docker run -d -p 8080:80 nginx)

# Step 3: Verify the running container
echo "Running containers:"
docker ps

# Wait for a few seconds so the container is up
sleep 5

# Step 4: Stop and remove the container
docker stop $container_id
docker rm $container_id

# Step 5: Remove the Nginx image
docker rmi nginx

echo "Nginx container and image removed successfully."

---

### **Screenshot**

<img width="1156" height="512" alt="Screenshot 2026-02-02 at 2 14 43 AM" src="https://github.com/user-attachments/assets/7a31dcad-9906-41da-9ced-5d1c760ae206" />

