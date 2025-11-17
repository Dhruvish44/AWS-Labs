# AWS Lab 30 – EKS Cluster Setup (Managed Kubernetes)

## 📘 Overview
This lab sets up a basic EKS cluster, node group, and deploys a sample Kubernetes application.

**Goal →** Understand the core Kubernetes workflow on AWS.

---

## 🏗️ Architecture Diagram
```text
                   ┌──────────────────────────┐
                   │      EKS Control Plane    │
                   │ (Managed by AWS, Highly   │
                   │   Available, Multi-AZ)    │
                   └───────────┬──────────────┘
                               │
                               ▼
                  Worker Node Group (EC2 or Fargate)
                               │
                               ▼
                          Kubernetes Pods
                               │
                               ▼
                         Sample Deployment
```

---

## 🚀 Steps Performed
```text
1️⃣ Install Required Tools
aws cli  
kubectl  
eksctl  
```

```text
2️⃣ Create EKS Cluster Using eksctl
eksctl create cluster \
--name dhruvish-eks \
--region ap-south-1 \
--nodes 2 \
--node-type t3.small
```

```text
3️⃣ Verify Cluster
kubectl get nodes
kubectl get pods -A
```

```text
4️⃣ Deploy Sample App
kubectl apply -f https://k8s.io/examples/application/deployment.yaml
kubectl apply -f https://k8s.io/examples/application/service.yaml
```

```text
5️⃣ Get Service External IP
kubectl get svc
Curl the IP:
curl http://<service-ip>
```

---

## 🧩 Verification
```bash
kubectl get nodes
kubectl get deploy
kubectl get pods
kubectl get svc
```

---

## 🧠 Key Takeaways
- EKS = managed Kubernetes control plane.  
- Nodes can run on EC2 OR Fargate.  
- kubectl drives the entire Kubernetes workflow.  
