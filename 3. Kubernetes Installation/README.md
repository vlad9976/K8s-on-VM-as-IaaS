# ⚙️ Kubernetes Setup Guide (Master Node)

<a href="https://kubernetes.io/" target="_blank"><img src="https://profilinator.rishav.dev/skills-assets/kubernetes-icon.svg" alt="Kubernetes" height="60" /></a>

---

## 📁 1. Shared Folder Configuration

🔹 Go to **Devices → Insert Guest Additions CD Image**  
<img src="images/Screenshot_11.png" width="800" height="600" />

🔹 Run the following commands:

```bash
sudo su
apt install bzip2 gcc make -y
mkdir --parents /media/cdrom
mount /dev/cdrom /media/cdrom
/media/cdrom/VBoxLinuxAdditions.run
reboot
```

📁 Your shared folder will appear at: `/media/sf<your_folder>`

---

## 🚫 2. Disable Swap

```bash
sudo sed -i '/\sswap\s/s/^/#/' /etc/fstab
sudo swapoff -a
free -h
```

📷 Should look like this:  
<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*XFIwxWHc9SMMXMcWb65-GQ.png" width="500" height="30" />

---

## ☸️ 3. Install Kubernetes (v1.25.4)

```bash
sudo apt-get update
sudo apt install curl apt-transport-https -y
curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/k8s.gpg
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update
sudo apt install kubelet=1.25.4-00 kubeadm=1.25.4-00 kubectl=1.25.4-00 -y
sudo apt-mark hold kubelet kubeadm kubectl
```

✅ Verify:

```bash
kubectl version --output=yaml
kubeadm version --output=yaml
```

📦 Repeat step 4 on:
- 🐧 Ubuntu → same setup
- 🪟 Windows → https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

---

## 🐳 4. Install Docker with CRI

```bash
sudo apt update
sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y containerd.io docker-ce docker-ce-cli

sudo mkdir -p /etc/systemd/system/docker.service.d
```

Create Docker daemon config:

```bash
sudo tee /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
```

✅ Verify:

```bash
docker --version
```

---

## 🧩 5. Install Mirantis CRI Adapter

```bash
VER=$(curl -s https://api.github.com/repos/Mirantis/cri-dockerd/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/v//g')
wget https://github.com/Mirantis/cri-dockerd/releases/download/v${VER}/cri-dockerd-${VER}.amd64.tgz
tar xvf cri-dockerd-${VER}.amd64.tgz
sudo mv cri-dockerd/cri-dockerd /usr/local/bin/

wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.service
wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.socket
sudo mv cri-docker.* /etc/systemd/system/
sudo sed -i 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service

sudo systemctl daemon-reload
sudo systemctl enable cri-docker.service
sudo systemctl enable --now cri-docker.socket
```

✅ Check:

```bash
cri-dockerd --version
systemctl status cri-docker.socket
```

---

## 🧷 6. Kubernetes Kernel & Networking Prerequisites

```bash
sudo tee /etc/modules-load.d/k8s.conf <<EOF
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

sudo tee /etc/sysctl.d/kubernetes.conf <<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF

sudo sysctl --system
```

✅ Confirm settings:

```bash
lsmod | grep br_netfilter
lsmod | grep overlay
sysctl net.bridge.bridge-nf-call-iptables net.bridge.bridge-nf-call-ip6tables net.ipv4.ip_forward
```

---

## 👾 7. Set Up Worker Nodes

Repeat all steps from this guide on your worker nodes:

- `worker-1`: 192.168.13.243
- `worker-2`: 192.168.13.244

---

## ✅ Continue Setup

👉 [Next: Worker Nodes 👾👾](../1.%20Virtual%20Machines/README.md)  
👉 [Next: Cluster Installation 🧱](../4.%20Cluster%20Installation/README.md)
