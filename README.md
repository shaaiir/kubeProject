# 🧩 MongoDB + Mongo Express on Kubernetes (Minikube Setup)

This project demonstrates how to deploy **MongoDB** and **Mongo Express** on a local Kubernetes cluster using **Minikube** and **kubectl**.  
It uses Kubernetes objects like **Deployments**, **Services**, **Secrets**, and **ConfigMaps** to create a secure and fully functional environment.

---

## 🚀 Project Structure

kubeProject/
├── mongo.yaml # MongoDB Deployment and Service
├── mongo-express.yaml # Mongo Express Deployment and Service
├── mongo-secret.yaml # Secret storing MongoDB credentials
├── mongo-configmap.yaml # ConfigMap with MongoDB environment variables

---

## 🧠 Prerequisites

Before you begin, make sure you have:

1. **Minikube** installed  
   👉 [Install Guide](https://minikube.sigs.k8s.io/docs/start/)

   ```bash
   minikube version
kubectl installed
👉 Install Guide
kubectl version --client
A working Docker environment (Minikube uses it internally).
🧰 Step-by-Step Deployment Guide
1️⃣ Start Minikube
minikube start
(Optional: verify cluster info)
kubectl cluster-info
2️⃣ Apply Kubernetes Configurations
Apply all YAML files to your cluster:
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo-configmap.yaml
kubectl apply -f mongo.yaml
kubectl apply -f mongo-express.yaml
3️⃣ Check Deployment Status
Verify all pods and services are running:
kubectl get all
Expected output (example):
NAME                                 READY   STATUS    RESTARTS   AGE
pod/mongo-depl-85ffbc9879-gq98g      1/1     Running   0          2m
pod/mongo-express-6b7d59d6f6-pf8f8   1/1     Running   0          2m

NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/mongo-service   ClusterIP   10.98.32.14      <none>        27017/TCP        2m
service/mongo-express   NodePort    10.105.218.132   <none>        8081:30000/TCP   2m
4️⃣ Access Mongo Express UI
Get the NodePort URL using:
minikube service mongo-express --url
Output example:
http://127.0.0.1:30000
Visit the URL in your browser to access Mongo Express Dashboard 🎉
5️⃣ Cleanup (optional)
To delete everything:
kubectl delete -f mongo-express.yaml
kubectl delete -f mongo.yaml
kubectl delete -f mongo-configmap.yaml
kubectl delete -f mongo-secret.yaml
Stop Minikube:
minikube stop
