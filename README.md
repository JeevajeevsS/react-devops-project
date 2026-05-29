# 🚀 React DevOps CI/CD Project

This project demonstrates a complete end-to-end CI/CD pipeline using:

- React.js
- Docker
- Docker Hub
- Jenkins
- GitHub Webhooks
- AWS EC2

The application is containerized using Docker and automatically deployed to AWS EC2 using Jenkins pipelines.

---

# 📌 Project Architecture

Developer Pushes Code → GitHub → Jenkins Pipeline → Docker Build → Docker Hub → AWS EC2 Deployment

---

# 🛠 Technologies Used

| Technology | Purpose |
|------------|---------|
| React.js | Frontend Application |
| Docker | Containerization |
| Docker Hub | Image Registry |
| Jenkins | CI/CD Automation |
| GitHub | Source Code Management |
| AWS EC2 | Cloud Hosting |
| Linux | Server Environment |
| SSH | Remote Deployment |

---

# 📂 Project Structure

```bash
react-devops-project/
│
├── src/
├── public/
├── Dockerfile
├── Jenkinsfile
├── .dockerignore
├── package.json
└── README.md
```

---

# ⚙️ CI/CD Workflow

## 1️⃣ Developer Pushes Code

```bash
git push origin main
```

---

## 2️⃣ GitHub Webhook Triggers Jenkins

GitHub automatically triggers Jenkins pipeline.

---

## 3️⃣ Jenkins Pipeline Executes

Pipeline stages:

- Clone Code
- Build Docker Image
- Push Docker Image to Docker Hub
- Deploy to AWS EC2

---

## 4️⃣ Docker Image Build

Jenkins builds Docker image using:

```bash
docker build -t jeevas12/react-app:latest .
```

---

## 5️⃣ Push Image to Docker Hub

```bash
docker push jeevas12/react-app:latest
```

---

## 6️⃣ Automatic Deployment to AWS EC2

Jenkins connects to EC2 using SSH and:

- Stops old container
- Removes old container
- Pulls latest Docker image
- Starts updated container

---

# 🐳 Docker Commands Used

## Build Image

```bash
docker build -t react-app .
```

## Run Container

```bash
docker run -d -p 3000:3000 react-app
```

## View Running Containers

```bash
docker ps
```

---

# ☁️ AWS EC2 Setup

Two EC2 instances were used:

| Server | Purpose |
|--------|---------|
| Jenkins EC2 | CI/CD Server |
| App EC2 | Application Hosting |

---

# 🔐 Jenkins Credentials

Docker Hub credentials were securely stored inside Jenkins Credentials Manager.

---

# 🚀 Features

✅ Dockerized React Application  
✅ Jenkins CI/CD Pipeline  
✅ GitHub Webhook Automation  
✅ Automatic Docker Builds  
✅ Automatic EC2 Deployment  
✅ Cloud Hosted Application  
✅ End-to-End Automation

---

# 🧠 Problems Faced & Solutions

## 1. Docker Build Failure

### Issue
`node_modules` caused Docker build errors.

### Solution
Added `.dockerignore`

```bash
node_modules
```

---

## 2. Jenkins Node Offline

### Issue
Low disk space caused Jenkins executors to stop.

### Solution
- Cleaned Docker cache
- Forced node online using Script Console

---

## 3. Docker Permission Issues

### Issue
Docker permission denied on EC2.

### Solution

```bash
sudo usermod -aG docker ec2-user
```

---

## 4. Jenkins Credential Error

### Issue
Jenkins could not find Docker credentials.

### Solution
Matched Jenkins credential ID with Jenkinsfile.

---

## 5. GitHub Webhook Not Triggering

### Issue
Automatic builds were not starting.

### Solution
Configured GitHub webhook:

```bash
http://<JENKINS-IP>:8080/github-webhook/
```

---

# 📸 Output

The React application is successfully deployed on AWS EC2 with automatic CI/CD deployment.

---

# 📈 Future Improvements

- Add HTTPS using Nginx
- Add Custom Domain
- Kubernetes Deployment
- Monitoring & Logging
- Terraform Infrastructure
- Jenkins Shared Libraries

---

# 👨‍💻 Author - Jeeva

Developed as a DevOps learning project to understand:

- CI/CD Pipelines
- Docker Workflows
- Cloud Deployment
- Infrastructure Automation

---

# ⭐ Conclusion

This project demonstrates a fully automated CI/CD pipeline using Jenkins, Docker, GitHub, and AWS EC2.

Any code pushed to GitHub is automatically built, containerized, and deployed to a live AWS server.