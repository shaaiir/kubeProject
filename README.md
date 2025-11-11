text
# 🍃 MongoDB + Mongo Express on Kubernetes (Minikube Setup)

[![Kubernetes](https://img.shields.io/badge/kubernetes-blue.svg)](https://kubernetes.io/)
[![Minikube](https://img.shields.io/badge/minikube-orange.svg)](https://minikube.sigs.k8s.io/)
[![MongoDB](https://img.shields.io/badge/mongodb-4.4+-green.svg)](https://www.mongodb.com/)
[![Mongo Express](https://img.shields.io/badge/mongo--express-1.0+-yellow.svg)](https://github.com/mongo-express/mongo-express)
[![Python](https://img.shields.io/badge/python-3.7%2B-blue.svg)](https://www.python.org/)
[![MIT License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

> This project demonstrates how to deploy **MongoDB** and **Mongo Express** on a local Kubernetes cluster using **Minikube** and **kubectl**.  
It uses Kubernetes objects like **Deployments**, **Services**, **Secrets**, and **ConfigMaps** to create a secure and production-ready environment.

---

## 📚 Table of Contents
- [Project Overview](#project-overview)
- [Architecture Diagram](#architecture-diagram)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
- [Verify Deployment](#verify-deployment)
- [Access Application](#access-application)
- [Cleanup](#cleanup)
- [Common Commands Reference](#common-commands-reference)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Maintainer](#maintainer)
- [Screenshots](#screenshots)

---

## 🧠 Project Overview

This Kubernetes project deploys **MongoDB** as a backend database and **Mongo Express** as a web-based MongoDB admin interface.  
Ideal for local Kubernetes learning, testing, and demonstrations on **Minikube**.

---

## 🔧 Key Features

- MongoDB database running inside Kubernetes
- Mongo Express web dashboard for database management
- Kubernetes Secrets for storing credentials securely
- ConfigMaps for database configuration
- NodePort Service for external access

---

## 🏗️ Architecture Diagram

+-----------------------------------------------------------+

Minikube Cluster
+----------------+ +--------------------------+
+----------------+ +--------------------------+
^ ^
Secret (Auth) ConfigMap (Env Vars)
+-----------------------------------------------------------+
text

---

## 📁 Project Structure

kubeProject/
├── mongo.yaml # MongoDB Deployment & Service
├── mongo-express.yaml # Mongo Express Deployment & Service
├── mongo-secret.yaml # Secret storing MongoDB credentials
└── mongo-configmap.yaml # ConfigMap with MongoDB environment variables

text

---

## 🧩 Kubernetes Components Overview

| File Name             | Object Type      | Purpose                                    |
|-----------------------|------------------|--------------------------------------------|
| `mongo.yaml`          | Deployment + Service | Runs MongoDB Pod and exposes it internally |
| `mongo-express.yaml`  | Deployment + Service | Web-based MongoDB management               |
| `mongo-secret.yaml`   | Secret              | Stores MongoDB username and password securely|
| `mongo-configmap.yaml`| ConfigMap           | Contains environment variables for MongoDB  |

---

## ⚙️ Prerequisites

Before you begin, ensure the following are installed:

| Tool       | Purpose                     | Install Command              |
|------------|-----------------------------|------------------------------|
| [Minikube](https://minikube.sigs.k8s.io/docs/start/) | Local Kubernetes cluster     | `brew install minikube`      |
| [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) | Kubernetes CLI tool         | `brew install kubectl`       |
| Docker     | Container runtime for Minikube| -                           |

Verify installations:
minikube version
kubectl version --client
docker --version

text

---

## 🚀 Setup Instructions

**Step 1: Start Minikube**
minikube start

(Optional: verify the cluster)
kubectl cluster-info
kubectl get nodes

text

**Step 2: Apply Kubernetes Manifests**
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo-configmap.yaml
kubectl apply -f mongo.yaml
kubectl apply -f mongo-express.yaml

text

**Step 3: Verify Deployment**
kubectl get all

Detailed status
kubectl describe pod <pod-name>
kubectl logs <pod-name>

text

---

## 🌐 Access Application

Expose the Mongo Express dashboard using Minikube:

minikube service mongo-express-service

text

This command will open Mongo Express in your browser.  
Alternatively:
minikube service list

text
Copy the URL for `mongo-express-service` and open it manually.

---

## 🧹 Cleanup

Remove all created resources:
kubectl delete -f mongo-express.yaml
kubectl delete -f mongo.yaml
kubectl delete -f mongo-configmap.yaml
kubectl delete -f mongo-secret.yaml

text
Stop Minikube:
minikube stop

text

---

## 🧩 Common Commands Reference

| Task                 | Command                                  |
|----------------------|------------------------------------------|
| View running Pods    | `kubectl get pods`                       |
| View Services        | `kubectl get svc`                        |
| Delete a Pod         | `kubectl delete pod <pod-name>`          |
| Restart Deployment   | `kubectl rollout restart deployment <deployment-name>` |
| View Logs            | `kubectl logs <pod-name>`                |
| Describe Resource    | `kubectl describe <resource> <name>`     |

---

## 🛠 Troubleshooting

| Issue                       | Cause                        | Fix/Checks                                  |
|-----------------------------|------------------------------|---------------------------------------------|
| Pods stuck in Pending       | Insufficient resources       | `minikube stop && minikube start`           |
| Mongo Express can’t connect | Wrong secret/config          | Verify environment variables in YAML         |
| CrashLoopBackOff            | Bad container config         | Check logs: `kubectl logs <pod>`            |
| Service not opening         | Port not exposed             | Use `minikube service list`                 |

---

## 💡 Contribution Guidelines

Contributions are welcome!  
- Fork the repository  
- Create a new branch: `git checkout -b feature-name`  
- Commit your changes: `git commit -m "Add new feature"`  
- Push the branch: `git push origin feature-name`  
- Open a Pull Request 🎉  

---

## 📜 License

This project is licensed under the **MIT License** — feel free to use and modify it.

---

## 👨‍💻 Maintainer

**Shahir Ali**  
📧 [Contact on GitHub](https://github.com/shaaiir)  
💼 Cybersecurity & Cloud Enthusiast | DevSecOps Researcher

---

## 🖼️ Screenshots

<!-- Add local screenshots using Markdown image syntax -->
![MongoDB and Mongo Express on Kubernetes demo](./screenshots/mongo-express-ui.png)
![Project Structure](./screenshots/project-structure.png)

<!-- More screenshots can be added to showcase setup and dashboards -->

---

## 🌐 Repository

GitHub Repo: [https://github.com/shaaiir/kubeProject](https://github.com/shaaiir/kubeProject)

---

> For help, troubleshooting, or feature requests, please open an Issue/Pull Request or contact [support@cloudbyte.com](mailto:support@cloudbyte.com).
