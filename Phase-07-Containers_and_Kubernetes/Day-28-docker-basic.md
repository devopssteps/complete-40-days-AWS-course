
## Docker Basic With Hands On Example 


What is Docker?
 - A platform for developing, shipping, and running applications inside lightweight containers.

Image vs Container
 - Image: Blueprint
 - Container: Running instance of an image

Dockerfile
 - Instructions to build an image

Docker Hub
 - Public registry for storing and sharing Docker images

Docker Compose
 - Tool for defining and running multi-container Docker apps

Volumes
 - For persistent storage

Networking
 - Bridge, host, none, and custom networks

## 🛠 Hands-On Demo Structure (Beginner Friendly)


### ✅ 1. Run Your First Container
```sh
docker run -d -p 8082:80 httpd
```

### ✅ 2. Pull and Run a Web Server (e.g., Nginx)
```sh
docker pull nginx
docker run -d -p 8080:80 nginx
```

### ✅ 3. Create a Dockerfile and Build an Image
```sh
FROM ubuntu:latest

RUN apt-get update && apt-get install -y nginx
WORKDIR /var/www/html/
COPY index.html .
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```
Create the image
```sh
docker build -t d3 .
```
Run the file
```sh
docker run -d -p 8081:80 d3
```

### ✅ 4. Docker Compose Example
docker-compose.yml
```sh
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```
Run:
```sh
docker-compose up
```

### Another docker file example
Create Dockerfile
```sh
# Use base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy app files
COPY app.py .

# Run app
CMD ["python", "app.py"]
```

Create app.py file
```sh
print("Hello from inside the container!")
```
Build & Run
```sh
docker build -t my-python-app .
docker run my-python-app
```

# Install Docker
# 1. Update your existing list of packages
sudo apt update && sudo apt upgrade -y
# 2. Install prerequisite packages that let apt use packages over HTTPS
sudo apt install -y ca-certificates curl gnupg
# 3. Add Docker’s official GPG key
```sh
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://docker.com -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
# 4. Set up the Docker repository
```sh
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://docker.com \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/etc/apt/sources.list.d/docker.list > /dev/null
```
# 5. Update the package index again with Docker packages included
sudo apt update
# 6. Install Docker Engine, CLI, and Docker Compose
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

------------------------------
## Crucial Post-Installation Step (Optional but Recommended)
By default, you have to use sudo every time you run a docker command. To run Docker commands without sudo, add your user account to the docker group.

# Add your current user to the docker group
sudo usermod -aG docker $USER
# Apply the new group membership immediately (or restart your terminal)
newgrp docker

## Verify the Installation
Test that Docker is installed correctly and running by pulling a tiny test image:

docker run hello-world


















