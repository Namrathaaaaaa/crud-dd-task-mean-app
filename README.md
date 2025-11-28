# 🚀 CRUD-DD Task — MEAN App

**Video URL:** 

## 🚀 Project Overview

This repository demonstrates a full-stack CRUD application built with the MEAN stack (MongoDB, Express, Angular, Node.js) and a production-ready DevOps workflow. It includes:

- Local dev instructions for frontend and backend
- Containerization with Docker and orchestration via Docker Compose (`./docker-compose.yaml`)
- Static frontend served through Nginx (`./nginx.conf`)
- Jenkins pipeline (`./jenkinsfile`) for building/pushing Docker images and deploying to an AWS EC2 host

Use this README to run locally, build images, and follow the CI/CD deployment flow. Add your demo video and screenshots to make this portfolio-ready.

---

**Quick Links**

- Backend Dockerfile: [./backend/Dockerfile](./backend/Dockerfile)
- Frontend Dockerfile: [./frontend/Dockerfile](./frontend/Dockerfile)
- Docker Compose: [./docker-compose.yaml](./docker-compose.yaml)
- Nginx config: [./nginx.conf](./nginx.conf)
- Jenkins pipeline: [./jenkinsfile](./jenkinsfile)


---

## 🧱 Tech Stack

- Angular (frontend)
- Node.js + Express (backend)
- MongoDB (database)
- Nginx (reverse proxy)
- Docker & Docker Compose
- Jenkins (CI/CD), Slack notifications, AWS EC2

---

## 📂 Folder Structure (high level)

- `backend/` — Node/Express backend and `Dockerfile`
- `frontend/` — Angular frontend and `Dockerfile`
- `docker-compose.yaml` — Compose manifest (services, networks, volumes)
- `nginx.conf` — Nginx reverse proxy configuration
- `jenkinsfile` — Jenkins declarative pipeline

---

## 🐳 Docker & Containers

I removed the inline Dockerfile contents here — please click the links above to view the exact Dockerfiles in the repository. The links point to the source of truth so your README stays clean while keeping the code accessible.

If you want to build locally, run the build commands from the service folders (see the Dockerfiles for the exact steps and dependencies).

---

## 🔧 Docker Compose Setup

The Compose manifest controls service wiring and ports. Open it here: [./docker-compose.yaml](./docker-compose.yaml).

High-level notes (from the file):

- Backend image: `namratha3/dd-mean-backend` — container port `8080`, mapped to host `8083` in the file.
- Frontend image: `namratha3/dd-mean-frontend` — served via Nginx on host port `80`.
- Mongo: `mongo:5` with a named volume `mongo_data`.

To start the stack locally: run `docker compose up -d` from the repo root (see the compose file for details).

---

## 🌐 Nginx Reverse Proxy

The Nginx configuration is available here: [./nginx.conf](./nginx.conf). It serves the built Angular assets and proxies `/api/` to the backend service (see the file for the precise `proxy_pass` target).

---

## 🔄 Jenkins CI/CD Pipeline

The pipeline is included in the repo: [./jenkinsfile](./jenkinsfile). Sample/summary:

- Uses Jenkins declarative pipeline and `docker buildx` to build and push images to Docker Hub.
- Sends Slack notifications via a credential `slack-cred`.
- SSHs to an EC2 host (uses `aws-ssh-key`) to pull updated images and restart the Compose stack.

Please open the file to inspect the exact commands and environment variables.

---

## ☁️ AWS Deployment Guide

The Jenkins pipeline deploys to an EC2 host by updating the `docker-compose.yaml` on the host and running `docker compose pull` + `docker compose up -d`. See `./jenkinsfile` for the exact commands and target host (`AWS_IP`) used in the pipeline.

Manual setup checklist (create a small `docs/aws-setup.md` if you want these steps saved):

- Install Docker and Docker Compose on the EC2 instance.
- Clone this repository into `/home/ubuntu/crud-dd-task-mean-app` on the EC2 instance.
- Ensure the Jenkins SSH key (`aws-ssh-key`) is authorized for the EC2 user.
- Verify Docker can be run by the deployment user (add to `docker` group or use `sudo`).

---

## 📸 Screenshots & Demo Video (placeholders)

Add your recorded demo video and screenshots into `./docs/` (recommended) and update these links.

- Demo video: `./docs/demo.mp4` — link: [./docs/demo.mp4](./docs/demo.mp4)
- Jenkins CI screenshot: `./docs/screenshots/jenkins-build.png`
- Docker build & push logs: `./docs/screenshots/docker-build.png`
- Deployed UI screenshot: `./docs/screenshots/ui-home.png`
- Nginx/infrastructure diagram: `./docs/screenshots/nginx-setup.png`

Example Markdown to embed an image (replace path with your screenshot): `![Jenkins build](./docs/screenshots/jenkins-build.png)`

---

## ✅ Step-by-step Setup & Deployment (quick start)

1. Clone the repo: `git clone https://github.com/Namrathaaaaaa/crud-dd-task-mean-app.git` and `cd crud-dd-task-mean-app`.
2. Backend (development): check `./backend/Dockerfile` and run the commands indicated there; the app entrypoint is `server.js`.
3. Frontend (development): check `./frontend/Dockerfile` and your Angular project files; typical dev command is `ng serve --port 8081`.
4. Full stack (containers): run `docker compose up -d` from the repository root; consult `./docker-compose.yaml` for ports and images.
5. CI/CD: configure Jenkins using `./jenkinsfile`; ensure credentials `docker-cred`, `slack-cred`, and `aws-ssh-key` exist in Jenkins.

---

## 🏁 Final Notes

- This README intentionally avoids embedding large code blocks — it links to the authoritative files in the repository instead. Click the links at the top of this document to view the exact Dockerfiles, Compose manifest, Nginx config, and Jenkins pipeline.
- Replace `ADD_YOUR_DEPLOYMENT_URL_HERE` with your live URL and add screenshots/video to `./docs/` to make this portfolio-ready.
- Want me to create `./docs/` and add image placeholders (empty files) or convert the Jenkins pipeline to GitHub Actions? I can do that next.

Good luck — ship it! 🚀
restart: unless-stopped
