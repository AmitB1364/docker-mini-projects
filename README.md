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
   git clone [https://github.com/YOUR_USERNAME/docker-mini-project.git](https://github.com/YOUR_USERNAME/docker-mini-project.git)
   cd docker-mini-project
