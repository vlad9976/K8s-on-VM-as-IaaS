# 🧠 VirtualBox Master 🤖 & Workers 👾👾 Setup

<img src="../img/icons8-virtualbox-logo-96.png" width="60" /> <img src="../img/icons8-ubuntu-96.png" width="60" /> <img src="../img/icons8-cluster-96.png" width="60" />

---

## 🎯 Goal

Set up a local VM-based Kubernetes environment by first creating the Master node, then cloning or replicating it for Worker nodes using VirtualBox and Ubuntu Server 22.04.

---

## 🪛 What You’ll Do

* ✅ Create 1 master and 2 worker VMs
* ✅ Configure network bridging so your VMs can talk to each other and the internet
* ✅ Allocate CPU, RAM, and storage resources appropriately
* ✅ Share folders for convenient file access

---

## 🧱 Step-by-Step VM Creation

### 🔽 0. Download Ubuntu Server

Download Ubuntu 22.04 ISO from the official site: <a href="https://ubuntu.com/download/server" target="_blank"> <img src="../img/icons8-ubuntu-96.png" height="40" /> </a>

---

### 🧰 1. Open VirtualBox > Click "New"

Give your VM a name and choose a directory for storage.

![Step 1](images/Screenshot_5.png)

---

### 🧠 2. Set Name & Location

Choose a clear name like `k8s-master` and select your desired storage location.

![Step 2](images/Screenshot_1.png)

---

### 🧠 3. Assign CPU & Memory

Recommend: 2 CPUs and 2048 MB RAM

![Step 3](images/Screenshot_2.png)

---

### 💾 4. Configure Disk Size

* Master Node: 20 GB
* Worker Nodes: 50 GB each

![Step 4](images/Screenshot_3.png)

---

### 🔌 5. Power Off VM to Configure Network

After creating the VM, shut it down before modifying the settings.

![Step 5](images/Screenshot_9.png)

---

### ⚙️ 6. Open VM Settings

Click on your VM > Settings

![Step 6](images/Screenshot_4.png)

---

### 🌐 7. Configure Network to "Bridged Adapter"

Ensures the VM gets a LAN IP address and internet access.

![Step 7](images/Screenshot_6.png)

---

### 📡 8. Choose Correct Network Interface

Use `ipconfig /all` on Windows to confirm your active network interface (e.g., Intel(R) Wi-Fi 6 AX201).

![Step 8](images/Screenshot_10.png)

---

### 📁 9. (Optional) Enable Shared Folders

Mount local folders to transfer bash scripts or configs easily.

![Step 9](images/Screenshot_12.png)

---

### 💾 10. Save All Settings

Make sure all changes are applied before booting the VM.

---

## ⏭️ Continue To...

### 👉 [Ubuntu Installation 🐧](../2.%20Ubuntu%20Installation/README.md)

Let’s install the OS and prepare it for Kubernetes! 🛠️
