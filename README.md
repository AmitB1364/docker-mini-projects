# docker-mini-projects
Containerize a Web Application, save container image and mount local drive to the container.

# Docker Web Server & Multi-Service Setup 🐳

A hands-on mini project demonstrating custom Docker containerization, dynamic host-to-container volume mounting, image commits, and multi-service orchestration using Supervisor.

## 📌 Project Overview

This repository demonstrates practical container management workflows:
- Running web servers (**Apache**) inside isolated containers.
- **Bind Mounting** local host directories (`/ami-docker`) into container root (`/var/www/html`) for live development without rebuilding images.
- Committing running container states into reusable custom Docker images.
- Managing multiple processes (**Apache + Index**) within a single container.

---

## 🛠️ Key Technical Features

- **Live Host Synchronization:** Modified files locally on macOS instantly reflect inside the running container volume.
- **Custom Image Building:** Created custom base configurations and committed runtime modifications using `docker commit`.
- **Port Mapping & Isolation:** Exposed traffic safely via custom port bindings (`8080:80`).

---

## 🚀 How to Run Locally

### Prerequisites
- [Docker Desktop](https://www.docker.com/) installed and running.

### Quick Start

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/docker-mini-project.git]
   cd docker-mini-project

Create a Dockerfile :
# Use the official Ubuntu image
FROM ubuntu:latest

# Copy your webpage into html public folder
COPY my-index.html /var/www/html/

# Expose port 80 to the outside world
EXPOSE 80

# Install Apache (Build Phase)
RUN apt-get update && \
    apt-get install -y apache2 && \
    rm -rf /var/lib/apt/lists/*

# Start Apache in the foreground (Runtime Phase)
CMD ["apache2ctl", "-D", "FOREGROUND"]


Build the custom Docker image:
docker build -t ubuntu .

Run container with a bind mount for live web updates:
docker run -d -p 7070:80 -v /Users/amitb/ami-docker:/var/www/html --name ubuntu-mount ubuntu-apache-installed sleep infinity

Verify the application:
http://localhost:7070/my-index.html
&
http://localhost:7070


Key Docker Commands Used
# Check running containers
docker ps

# Shell into the active container
docker exec -it web-app /bin/bash

# Commit container changes to a new image tag
docker commit web-app my-custom-webserver:v2

# Push local custom docker image to github

Step 1: Create a GitHub Personal Access Token (PAT)
Docker cannot use your regular GitHub password to authenticate via the command line. You need a token
2. Click Generate new token (classic).
3. Give it a descriptive name and select the write:packages scope (this will automatically select read:packages as well).
4. Click Generate token and copy it immediately (you won't be able to see it again).

Step 2: Authenticate via Terminal
echo "YOUR_PERSONAL_ACCESS_TOKEN" | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin

Step 3: Tag Your Local Image
docker tag ubuntu-apache-installed:latest ghcr.io/YOUR_GITHUB_USERNAME/ubuntu-apache-installed:latest

Step 4: Push the Image to GitHub
docker push ghcr.io/amitb1364/ubuntu-apache-installed:latest 


Where to find container image it on GitHub
Once the transfer completes, navigate to your GitHub profile and click on the Packages tab along the top navigation bar (next to Repositories).

Install from the command line
docker pull ghcr.io/amitb1364/ubuntu-apache-installed:latest

