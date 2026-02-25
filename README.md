# 🚀 MEAN Stack DevOps Deployment with CI/CD

## 📌 Project Summary

This project demonstrates the complete DevOps lifecycle of a MEAN (MongoDB, Express, Angular, Node.js) application.

The application has been:

- Containerized using Docker
- Deployed on AWS EC2 (Ubuntu)
- Configured with Nginx Reverse Proxy
- Automated using GitHub Actions CI/CD
- Integrated with Docker Hub
- Verified with live auto-deployment testing

This setup replicates a real-world production deployment architecture.

---

# 🏗 Architecture Overview

User  
⬇  
Nginx (Port 80)  
⬇  
Frontend Container (Angular - Port 3000 → 80)  
⬇  
Backend Container (Node/Express - Port 8080)  
⬇  
MongoDB Container  

CI/CD Flow:

Developer → GitHub → GitHub Actions → Docker Hub → AWS EC2 → Auto Deploy

---

# 🛠 Technologies Used

| Layer | Technology |
|-------|------------|
| Frontend | Angular |
| Backend | Node.js + Express |
| Database | MongoDB |
| Containerization | Docker |
| Orchestration | Docker Compose |
| Cloud | AWS EC2 (Ubuntu) |
| Reverse Proxy | Nginx |
| CI/CD | GitHub Actions |
| Image Registry | Docker Hub |

---

# 🐳 Docker Implementation

## Backend

- Dockerfile created inside `backend/`
- Exposes port 8080
- Connected to MongoDB service inside Docker network

## Frontend

- Multi-stage Docker build
- Angular production build
- Served using Nginx (inside container)
- Exposes port 80 internally

## Docker Compose

File: `docker-compose.yml`

Services:

- mongodb
- backend
- frontend

Ports Mapping:

- 3000 → Frontend
- 8080 → Backend
- 27017 → MongoDB (internal)

---

# ☁ AWS EC2 Deployment

- Ubuntu EC2 instance launched
- Security Group configured:
  - Port 22 (SSH)
  - Port 80 (HTTP)
- Docker & Docker Compose installed
- Images pulled from Docker Hub
- Containers deployed using docker-compose

Application accessible at that time when EC2 running beacuse of dynamic public cause of the we have to change according to the public IP everytime after the running EC2 instance so we have add this public IP to secrets update and the reun again if we do not want this process so we have to use Elastic IP and domain name.

http://13.204.76.250

---

# 🌐 Nginx Reverse Proxy Setup

Nginx installed on EC2 host.

Configuration:

- `/` → Proxies to frontend (localhost:3000)
- `/api` → Proxies to backend (localhost:8080)

This ensures entire application runs through Port 80.

---

# 🔁 CI/CD Pipeline (GitHub Actions)

Workflow File:.github/workflows/deploy.yml

### Pipeline Trigger
- On push to `main` branch
- Manual trigger available (`workflow_dispatch`)

### Pipeline Steps

1. Checkout repository
2. Login to Docker Hub (using Access Token)
3. Build backend Docker image
4. Build frontend Docker image
5. Push images to Docker Hub
6. SSH into EC2
7. Pull latest images
8. Restart containers using docker-compose

---

# 🔐 Security Implementation

Sensitive credentials stored as GitHub Secrets:

- DOCKER_USERNAME
- DOCKER_PASSWORD (Access Token)
- EC2_HOST
- EC2_USER
- EC2_SSH_KEY

No credentials are hardcoded in repository.

---

# 🧪 CI/CD Verification Test

To verify automation:

1. Modified frontend UI text
2. Pushed code to GitHub
3. GitHub Actions pipeline executed
4. Docker images rebuilt and pushed
5. EC2 auto-deployed updated containers
6. Verified updated UI live on server

Result:
Successful automatic deployment without manual intervention.

---

# 🎯 Key Achievements

- End-to-end containerization
- Cloud deployment
- Reverse proxy configuration
- Full CI/CD automation
- Production-style architecture
- Real-time deployment verification

---

# 👨‍💻 Author

Gaurav Kumar  
DevOps & Cloud Engineering Enthusiast
