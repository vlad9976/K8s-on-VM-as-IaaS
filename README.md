# 🚀 Kubernetes Cluster on VirtualBox

<a href="https://kubernetes.io/" target="_blank"><img src="https://profilinator.rishav.dev/skills-assets/kubernetes-icon.svg" alt="Kubernetes" height="120" /></a> <img src="/img/metallb-icon-color.png" height="120" /> <img src="/img/icons8-nginx-accelerates-content-and-application-delivery-improves-security-96.png" height="120" /> <img src="/img/icons8-virtualbox-logo-96.png" height="120" />

---

## 🌟 Project Overview

Create a local Kubernetes cluster on **Ubuntu Server 22.04 LTS** using **VirtualBox**. The cluster mimics a real IaaS environment and includes:

* A master node and 2 worker nodes
* MetalLB as the LoadBalancer solution
* NGINX as the Ingress controller

---

## 🤔 Why Kubernetes?

Because between **K** and **S**, there are **8** letters. Simple as that! 😅

---

## 📖 Introduction

This guide walks you through spinning up your own Kubernetes cluster locally using VirtualBox VMs. By the end, you'll have a fully functional cluster with a load balancer and ingress controller to simulate cloud-native deployments.

---

## 🧰 Requirements

* 🖥️ VirtualBox (latest version)
* 💽 Ubuntu Server 22.04 ISO

---

## ⏱️ Steps Summary

### 1️⃣ Provision Virtual Machines

* **1 Master Node 🤖**
* **2 Worker Nodes 👾👾**

### 2️⃣ Install Kubernetes 1.25.4

* `kubelet` 1.25.4-00 🚤
* `kubectl` 1.25.4-00 🛠️
* `kubeadm` 1.25.4-00 🏭

### 3️⃣ Install Docker (CRI)

* Install Container Runtime Interface 🔧
* Configure with **Mirantis containerd** or Docker

### 4️⃣ Bootstrap the Cluster

* Configure `cri-dockerd.sock` for image pulls
* Initialize Kubernetes master node with `kubeadm init`

### 5️⃣ Join Worker Nodes 🔌

* Use the `kubeadm join` command on worker nodes

### 6️⃣ Deploy MetalLB 🌐

* A bare-metal LoadBalancer implementation

### 7️⃣ Deploy NGINX Ingress Controller 🌍

* Manage external access via HTTP/HTTPS

---

## 📦 Start Here

### 🧠 [Master Node Setup 🤖](./1.%20Virtual%20Machines/README.md)

Click the link above to begin configuring your master node. Each step is fully explained in the respective subdirectories.

---

## 🧭 Next Steps

Once your cluster is up and running:

* Test deploying sample apps
* Configure ingress rules
* Add persistent volumes

Happy Clustering! ☸️💻
