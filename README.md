# MEAN Stack DevOps Assignment

This project is a full stack CRUD application using MongoDB, Express, Angular 15 and Node.js.
In this task I deployed the application using Docker, Docker Compose, Jenkins CI/CD and Nginx reverse proxy on AWS EC2.

The app allows user to create tutorials, update, delete and search by title.

---

## Tech Used

* Angular 15 (frontend)
* Node.js + Express (backend REST API)
* MongoDB database
* Docker & Docker compose
* Jenkins pipeline (CI/CD)
* Nginx reverse proxy
* AWS EC2 (Ubuntu)

---

## Architecture Flow

Developer push code → Jenkins build docker images → push to DockerHub → EC2 pulls latest images → containers restart → application live on port 80

---

## Setup Steps (Manual)

### 1. Clone repository

git clone https://github.com/Sagartikare/crud-dd-task-mean-app.git

### 2. Run using docker compose

docker-compose up -d

App will run on:
http://SERVER-IP

---

## Docker Images

Backend Image: sagartikare935335/mean-backend
Frontend Image: sagartikare935335/mean-frontend

---

## CI/CD Pipeline (Jenkins)

Pipeline stages:

1. Checkout code from GitHub
2. Build backend docker image
3. Build frontend docker image
4. Login DockerHub
5. Push images
6. Pull latest code on server
7. Restart containers using docker-compose

Whenever code is pushed → Jenkins automatically deploys new version.

---

## Nginx Reverse Proxy

Port 80 → Angular frontend
/api → Backend API

So user only accesses:
http://SERVER-IP

---

## Screenshots

## Jenkins Pipeline

Pipeline executed successfully with all stages completed.

![Pipeline Success](screenshots/jenkins-success.png)

---

## Docker Images in DockerHub

Both frontend and backend images pushed successfully.

![DockerHub Images](screenshots/dockerhub.png)

---

## Running Containers on EC2

All containers are up and running.

![Docker PS](screenshots/docker-ps.png)

---

## Application Working UI

CRUD operations working properly.

![Application UI](screenshots/app-ui_1.png)
![Application UI](screenshots/app-ui_2.png)

---

## Notes

At first frontend was not calling backend because localhost was used.
Changed API URL to relative path `/api/tutorials` so nginx proxy forwards to backend correctly.

---

## Author

Sagar Tikare
DevOps Internship Assignment
