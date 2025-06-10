# 🐧 Ubuntu Server 22.04.3 Installation Guide

<img src="../img/icons8-ubuntu-96.png" width="60" height="60" /> <img src="../img/icons8-install-64.png" width="60" height="60" /> 

---

## ⚙️ Step-by-Step Installation

### 1️⃣ Start your Virtual Machine

Power up the VM you created in VirtualBox. Make sure the ISO is mounted.

![Start VM](images/Screenshot_12.png)

---

### 2️⃣ Begin Ubuntu Server Installation

You'll see the Ubuntu installation screen. Follow the wizard to begin setup.

![Install Ubuntu](images/Screenshot_2.png)

---

### 3️⃣ IP Address via Bridge Adapter

Ubuntu will obtain a bridged IP (e.g., `192.168.x.x`) so it lives on the same network as your host.

![IP Bridged](images/Screenshot_3.png)

---

### 4️⃣ Skip LVM Group Setup

LVM is optional; for simplicity, you can skip it unless you have advanced needs.

![Skip LVM](images/Screenshot_4.png)

---

### 5️⃣ Set Username, Password & Hostname

Choose a meaningful username, secure password, and a unique machine name (e.g., `k8s-master`).

![Set Username](images/Screenshot_5.png)

---

### 6️⃣ Optional: Install OpenSSH

This lets you connect via SSH. Highly recommended! 🔐

![Install OpenSSH](images/Screenshot_6.png)

---

### 7️⃣ Wait for Installation to Complete ⏳

Sit back and relax while Ubuntu gets installed. Once prompted, reboot your machine.

---

## ✅ Post-Install Checks

After the reboot, login with the credentials you created and run the following:

### 🧪 Verify Host Connectivity

```bash
ping <your-host-IP>
```

### 🌐 Test Internet Access

```bash
curl www.google.com
```

### 📡 Check Network Interfaces

```bash
ip a
```

If all tests pass ✅✅✅, your VM is ready for the next step!

---

## ⏭️ Continue To...

### 🐳☸️ [Kubernetes & Docker Setup](../3.%20Kubernetes%20Installation/README.md)

Let’s install Docker and Kubernetes and turn this VM into a container powerhouse!

---
