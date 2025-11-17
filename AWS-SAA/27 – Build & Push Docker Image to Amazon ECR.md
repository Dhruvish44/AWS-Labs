# AWS Lab 27 – Build & Push Docker Image to Amazon ECR

## 📘 Overview
This lab covers building a Docker image locally, tagging it, authenticating with ECR, and pushing it to a private ECR repository.

**Goal →** Store your container images securely inside AWS ECR.

---

## 🏗️ Architecture Diagram
```text
Developer Machine
     │ (docker push)
     ▼
Amazon ECR Repository
     │ (pull)
     ▼
ECS / EKS / Fargate Tasks
```

---

## 🚀 Steps Performed
```text
1️⃣ Create ECR Repository
ECR → Create Repository
Name: dhruvish-web
Tag immutability: Enabled (recommended)
Scan on push: Enabled
```

```text
2️⃣ Authenticate Docker to ECR
aws ecr get-login-password --region ap-south-1 \
| docker login --username AWS --password-stdin <AWS_Account_ID>.dkr.ecr.ap-south-1.amazonaws.com
```

```text
3️⃣ Create Simple Dockerfile
Dockerfile:
FROM nginx:latest
COPY index.html /usr/share/nginx/html
```

Create index.html:
echo "Hello from ECR Deployment - $(date)" > index.html
```

```text
4️⃣ Build Docker Image
docker build -t dhruvish-web .
```

```text
5️⃣ Tag Image for ECR
docker tag dhruvish-web:latest <AWS_Account_ID>.dkr.ecr.ap-south-1.amazonaws.com/dhruvish-web:latest
```

```text
6️⃣ Push to ECR
docker push <AWS_Account_ID>.dkr.ecr.ap-south-1.amazonaws.com/dhruvish-web:latest
```

---

## 🧩 Verification
```bash
aws ecr list-images --repository-name dhruvish-web
```

Output should show:
```
IMAGE TAG: latest
IMAGE DIGEST: sha256:xxxx
```

---

## 🧠 Key Takeaways
- ECR stores container images securely.  
- Lifecycle policies help manage old images.  
- Image scanning improves security posture.  
