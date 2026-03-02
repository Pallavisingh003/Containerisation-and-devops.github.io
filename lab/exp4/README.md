# Experiment 4: Docker Essentials
---
Dockerfile .dockerignore tagging publishing
Part 1: Containerizing Applications with Dockerfile
Step 1: Create a Simple Application
Python Flask App:

mkdir my-flask-app
cd my-flask-app
app.py:

from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello from Docker!"

@app.route('/health')
def health():
    return "OK"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
requirements.txt:

Flask==2.3.3
Step 2: Create Dockerfile
Dockerfile:

# Use Python base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements file
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY app.py .

# Expose port
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]

Part 2: Using .dockerignore
Step 1: Create .dockerignore File
.dockerignore:

# Python files
__pycache__/
*.pyc
*.pyo
*.pyd

# Environment files
.env
.venv
env/
venv/

# IDE files
.vscode/
.idea/

# Git files
.git/
.gitignore

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/

# Test files
tests/
test_*.py
Step 2: Why .dockerignore is Important
Prevents unnecessary files from being copied
Reduces image size
Improves build speed
Increases security

2/12

Part 3: Building Docker Images
Step 1: Basic Build Command
# Build image from Dockerfile
docker build -t my-flask-app .

# Check built images
docker images
Step 2: Tagging Images
# Tag with version number
docker build -t my-flask-app:1.0 .

# Tag with multiple tags
docker build -t my-flask-app:latest -t my-flask-app:1.0 .

# Tag with custom registry
docker build -t username/my-flask-app:1.0 .

# Tag existing image
docker tag my-flask-app:latest my-flask-app:v1.0
Step 3: View Image Details
# List all images
docker images

# Show image history
docker history my-flask-app

# Inspect image details
docker inspect my-flask-app
3/12

Part 4: Running Containers
Step 1: Run Container
# Run container with port mapping
docker run -d -p 5000:5000 --name flask-container my-flask-app

# Test the application
curl http://localhost:5000

# View running containers
docker ps

# View container logs
docker logs flask-container
Step 2: Manage Containers
# Stop container
docker stop flask-container

# Start stopped container
docker start flask-container

# Remove container
docker rm flask-container

# Remove container forcefully
docker rm -f flask-container
4/12

Part 5: Multi-stage Builds
Step 1: Why Multi-stage Builds?
Smaller final image size
Better security (remove build tools)
Separate build and runtime environments

Step 2: Simple Multi-stage Dockerfile
Dockerfile.multistage:

# STAGE 1: Builder stage
FROM python:3.9-slim AS builder

WORKDIR /app

# Copy requirements
COPY requirements.txt .

# Install dependencies in virtual environment
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN pip install --no-cache-dir -r requirements.txt

# STAGE 2: Runtime stage
FROM python:3.9-slim

WORKDIR /app

# Copy virtual environment from builder
COPY --from=builder /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Copy application code
COPY app.py .

# Create non-root user
RUN useradd -m -u 1000 appuser
USER appuser

# Expose port
EXPOSE 5000

# Run application
CMD ["python", "app.py"]
Step 3: Build and Compare
# Build regular image
docker build -t flask-regular .

# Build multi-stage image
docker build -f Dockerfile.multistage -t flask-multistage .

# Compare sizes
docker images | grep flask-

# Expected output:
# flask-regular     ~250MB
# flask-multistage  ~150MB (40% smaller!)
5/12

Part 6: Publishing to Docker Hub
Step 1: Prepare for Publishing
# Login to Docker Hub
docker login

# Tag image for Docker Hub
docker tag my-flask-app:latest username/my-flask-app:1.0
docker tag my-flask-app:latest username/my-flask-app:latest

# Push to Docker Hub
docker push username/my-flask-app:1.0
docker push username/my-flask-app:latest
Step 2: Pull and Run from Docker Hub
# Pull from Docker Hub (on another machine)
docker pull username/my-flask-app:latest

# Run the pulled image
docker run -d -p 5000:5000 username/my-flask-app:latest
6/12

Part 7: Node.js Example (Quick Version)
Step 1: Node.js Application
mkdir my-node-app
cd my-node-app
app.js:

const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
    res.send('Hello from Node.js Docker!');
});

app.get('/health', (req, res) => {
    res.json({ status: 'healthy' });
});

app.listen(port, () => {
    console.log(`Server running on port ${port}`);
});
package.json:

{
  "name": "node-docker-app",
  "version": "1.0.0",
  "main": "app.js",
  "dependencies": {
    "express": "^4.18.2"
  }
}
Step 2: Node.js Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install --only=production

COPY app.js .

EXPOSE 3000

CMD ["node", "app.js"]
Step 3: Build and Run
# Build image
docker build -t my-node-app .

# Run container
docker run -d -p 3000:3000 --name node-container my-node-app

# Test
curl http://localhost:3000
7/12

Part 8: Quick Practice Exercises
Exercise 1: Tagging Practice
# Create an image with three tags:
# 1. myapp:latest
# 2. myapp:v2.0
# 3. yourusername/myapp:production

# Solution:
docker build -t myapp:latest -t myapp:v2.0 -t username/myapp:production .
Exercise 2: Multi-stage for Node.js
# Create a multi-stage Dockerfile for Node.js that:
# 1. Uses builder stage for npm install
# 2. Creates final image with only production dependencies
# 3. Uses non-root user

# Hint:
# STAGE 1: FROM node:18-alpine AS builder
# STAGE 2: FROM node:18-alpine
# COPY --from=builder /app/node_modules ./node_modules
Exercise 3: Clean Build
# Build without cache and with .dockerignore
docker build --no-cache -t clean-app .

# Compare with cached build
time docker build -t cached-app .
8/12

Essential Docker Commands Cheatsheet
Command
Purpose
Example
docker build
Build image
docker build -t myapp .
docker run
Run container
docker run -p 3000:3000 myapp
docker ps
List containers
docker ps -a
docker images
List images
docker images
docker tag
Tag image
docker tag myapp:latest myapp:v1
docker login
Login to Dockerhub using username and password or token
echo "token" | docker login -u username --password-stdin
docker push
Push to registry
docker push username/myapp
docker pull
Pull from registry
docker pull username/myapp
docker rm
Remove container
docker rm container-name
docker rmi
Remove image
docker rmi image-name
docker logs
View logs
docker logs container-name
docker exec
Execute command
docker exec -it container-name bash
9/12

Common Workflow Summary
Development Workflow:
# 1. Create Dockerfile and .dockerignore
# 2. Build image
docker build -t myapp .

# 3. Test locally
docker run -p 8080:8080 myapp

# 4. Tag for production
docker tag myapp:latest myapp:v1.0

# 5. Push to registry
docker push myapp:v1.0
Production Workflow:
# 1. Pull from registry
docker pull myapp:v1.0

# 2. Run in production
docker run -d -p 80:8080 --name prod-app myapp:v1.0

# 3. Monitor
docker logs -f prod-app
10/12

Key Takeaways
Dockerfile defines how to build your image
.dockerignore excludes unnecessary files (important for security and performance)
Tagging helps version and organize images
Multi-stage builds create smaller, more secure production images
Docker Hub allows sharing and distributing images
Always test images locally before publishing

11/12

Cleanup
# Remove all stopped containers
docker container prune

# Remove unused images
docker image prune

# Remove everything unused
docker system prune -a

# SCREENSHORTS
<img width="506" height="51" alt="Screenshot 2026-02-20 at 11 16 18 AM" src="https://github.com/user-attachments/assets/61eb9686-7392-435c-826b-c85c96ee4d94" />
<img width="507" height="55" alt="Screenshot 2026-02-20 at 11 16 25 AM" src="https://github.com/user-attachments/assets/f61d861e-56f5-4a34-a100-fc6954d55d62" />
<img width="466" height="242" alt="Screenshot 2026-02-20 at 11 19 57 AM" src="https://github.com/user-attachments/assets/feb5b3d9-1929-45bd-907a-2e3cabbf547c" />
<img width="563" height="344" alt="Screenshot 2026-02-20 at 11 21 25 AM" src="https://github.com/user-attachments/assets/d7991ec1-b4be-4d97-a7fa-a95374af1d2c" />
<img width="554" height="37" alt="Screenshot 2026-02-20 at 11 21 37 AM" src="https://github.com/user-attachments/assets/c08e6fac-234a-44c6-9968-dd936ab663ed" />
<img width="560" height="62" alt="Screenshot 2026-02-20 at 11 22 11 AM" src="https://github.com/user-attachments/assets/2ab67b44-13a8-4d2e-8be8-d58cac1a2815" />
<img width="562" height="349" alt="Screenshot 2026-02-20 at 11 23 36 AM" src="https://github.com/user-attachments/assets/11a1f830-383d-43ac-8752-da3ffa7200c6" />
<img width="529" height="243" alt="Screenshot 2026-02-20 at 11 23 58 AM" src="https://github.com/user-attachments/assets/ce5940bb-7a05-4a3f-a086-57ddaadc3fcd" />
<img width="485" height="46" alt="Screenshot 2026-02-20 at 11 24 13 AM" src="https://github.com/user-attachments/assets/c556d908-24c5-4d1b-b897-84e313377728" />
<img width="570" height="266" alt="Screenshot 2026-02-20 at 11 25 00 AM" src="https://github.com/user-attachments/assets/9c08d9de-7785-4244-8ed9-c519b9f7c6b2" />
<img width="547" height="34" alt="Screenshot 2026-02-20 at 11 25 14 AM" src="https://github.com/user-attachments/assets/54adb5b6-97fa-4405-9b4d-05c57cb65e12" />
<img width="914" height="508" alt="Screenshot 2026-02-20 at 11 25 51 AM" src="https://github.com/user-attachments/assets/69d390ab-1be4-464d-97b6-90354c687d51" />
<img width="641" height="301" alt="Screenshot 2026-02-20 at 11 26 07 AM" src="https://github.com/user-attachments/assets/1038eb25-779e-4721-baab-c13338733648" />
<img width="566" height="101" alt="Screenshot 2026-02-20 at 11 28 23 AM" src="https://github.com/user-attachments/assets/2033e14d-b615-4e17-866b-a80a287ad92a" />
<img width="826" height="148" alt="Screenshot 2026-02-20 at 11 29 53 AM" src="https://github.com/user-attachments/assets/136633d6-5073-4a5d-8455-102ad2815865" />
<img width="572" height="92" alt="Screenshot 2026-02-20 at 11 30 49 AM" src="https://github.com/user-attachments/assets/39622e15-cafe-4cd6-8ef2-eba60f10cf21" />
<img width="1062" height="140" alt="Screenshot 2026-02-20 at 11 34 53 AM" src="https://github.com/user-attachments/assets/2ca7fa6a-75bb-4101-b4f1-530bbfaeda08" />
<img width="1059" height="366" alt="Screenshot 2026-02-20 at 11 35 16 AM" src="https://github.com/user-attachments/assets/134145d7-21f8-4c03-95dc-46eefeaddba0" />
<img width="1122" height="761" alt="Screenshot 2026-02-20 at 11 35 59 AM" src="https://github.com/user-attachments/assets/9adc50ce-9f13-4de3-8892-bcd5fe016907" />
<img width="842" height="367" alt="Screenshot 2026-02-20 at 11 41 55 AM" src="https://github.com/user-attachments/assets/0d089494-188d-485a-b8a2-be224d36830f" />
<img width="889" height="378" alt="Screenshot 2026-02-20 at 11 42 16 AM" src="https://github.com/user-attachments/assets/f70654f4-94b4-44e3-92b9-3dcc4094d9a4" />
<img width="858" height="132" alt="Screenshot 2026-02-20 at 11 42 51 AM" src="https://github.com/user-attachments/assets/817da431-d187-4eaa-b436-50a94e318f1a" />
<img width="882" height="408" alt="Screenshot 2026-02-20 at 11 47 00 AM" src="https://github.com/user-attachments/assets/630e6ed8-0ce8-4409-adb0-7f0759af8242" />
<img width="788" height="109" alt="Screenshot 2026-02-20 at 11 49 15 AM" src="https://github.com/user-attachments/assets/19b5ac64-7c58-46c7-b73d-ded47f9825b8" />
<img width="1440" height="52" alt="Screenshot 2026-03-02 at 4 04 21 PM" src="https://github.com/user-attachments/assets/771ed335-87fd-4fbf-9846-9173935b537b" />
<img width="1022" height="492" alt="Screenshot 2026-03-02 at 4 04 31 PM" src="https://github.com/user-attachments/assets/b495feb1-9b9f-4c1f-b27b-d20ff3c5f3a8" />

---
