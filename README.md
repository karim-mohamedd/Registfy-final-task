# 🚀 CI/CD Pipeline: Deploy NGINX to AWS ECS using GitHub Actions

## 📌 Overview

This project demonstrates a complete **CI/CD pipeline** that automatically builds, pushes, and deploys a containerized NGINX application to AWS ECS using GitHub Actions.

The pipeline is triggered on every push to the `main` branch and performs the following steps:

* Build Docker image
* Push image to Amazon ECR
* Update ECS Task Definition
* Deploy the new version to ECS Service

---

## 🏗️ Architecture

```
GitHub Push → GitHub Actions → Docker Build → Amazon ECR → Amazon ECS → Running NGINX
```

---

## 🧰 Technologies Used

* GitHub Actions (CI/CD)
* AWS ECS (Fargate)
* AWS ECR (Container Registry)
* Docker
* NGINX

---

## 📁 Project Structure

```
.
├── Dockerfile
└── .github/
    └── workflows/
        └── deploy.yml
```

---

## 🐳 Dockerfile

```Dockerfile
FROM nginx:latest
EXPOSE 80
```

---

## ⚙️ GitHub Actions Workflow

Location:

```
.github/workflows/deploy.yml
```

### Key Steps:

* Configure AWS credentials
* Login to Amazon ECR
* Build & push Docker image
* Fetch ECS task definition
* Update container image
* Deploy to ECS service

---

## 🔐 Required GitHub Secrets

Add the following secrets in your repository:

| Secret Name           | Description          |
| --------------------- | -------------------- |
| AWS_ACCESS_KEY_ID     | AWS Access Key       |
| AWS_SECRET_ACCESS_KEY | AWS Secret Key       |
| AWS_REGION            | AWS Region           |
| ECR_REPOSITORY        | ECR repository name  |
| ECS_CLUSTER           | ECS cluster name     |
| ECS_SERVICE           | ECS service name     |
| ECS_TASK_DEFINITION   | Task definition name |

---

## ☁️ AWS Setup

### 1. Create ECR Repository

* Store Docker images

### 2. Create ECS Cluster

* Use Fargate (serverless)

### 3. Create Task Definition

* Container name must match workflow (`nginx-container`)
* Image: nginx (initially)

### 4. Create ECS Service

* Run 1 task
* Enable public IP
* Allow port 80 in security group

---

## 🚀 How to Deploy

1. Push code to `main` branch:

   ```bash
   git add .
   git commit -m "deploy"
   git push origin main
   ```

2. GitHub Actions will:

   * Build Docker image
   * Push to ECR
   * Deploy to ECS

---

## 🌐 Access Application

After deployment:

* Go to ECS → Tasks
* Copy public IP
* Open in browser:

```
http://<public-ip>
```

You should see the NGINX welcome page 🎉

---

## ⚠️ Important Notes

* Container name in ECS **must match** `CONTAINER_NAME` in workflow
* Ensure IAM user has proper permissions (ECS + ECR)
* Monitor AWS billing to avoid unexpected charges

---

## 🔒 Security Best Practices

* Store credentials in GitHub Secrets
* Avoid hardcoding sensitive data
* Consider using OIDC instead of access keys

---

## 🧠 Future Improvements

* Use image tagging with commit SHA
* Add Application Load Balancer (ALB)
* Implement Blue/Green deployment
* Use AWS OIDC authentication
* Add monitoring & logging (CloudWatch)

---

## 📬 Author

**Karim Elwaraky**
Junior DevOps Engineer

---

## ⭐ Acknowledgment

This project is part of hands-on DevOps practice to build real-world CI/CD pipelines on AWS.
