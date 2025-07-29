# CI/CD with Jenkins, Docker, and AWS ECR

This project is a simple **Flask-based web application** that serves a static resume website styled with CSS. This process is fully **automated using a Jenkins Pipeline** and triggered by a **GitHub Push.**

## ✅ Technologies Used
- 🐍 **Python Flask**
- 🐳 **Docker**
- ☁️ **Amazon ECR** (Elastic Container Registry)
- ⚙️ **Jenkins** (automated builds & deployment)
- 💻 **GitHub** (source control )

Jenkins-Docker-Flask/ <br>
├── app.py # Flask application <br>
├── templates/ <br>
│ └── index.html # HTML page <br>
├── static/ <br>
│ └── style.css # CSS styling <br>
├── Dockerfile # For containerizing the app <br>
└── Jenkinsfile # Jenkins pipeline for CI/CD <br>

## 🚀 CI/CD Pipeline Overview

Every time you **push code to GitHub**, the pipeline:

1.  **Clones the GitHub repo**
2.  **Builds a Docker image**
3.  **Pushes the image to Amazon ECR**
4.  **Runs the Docker container** on the Jenkins host

## 📦 Docker Image

The Docker image is built using the provided `Dockerfile` and includes all dependencies to run the Flask app. It is tagged and pushed to **AWS ECR**.
