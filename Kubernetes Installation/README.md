# Kubernetes Installation

<h3>Configure share folder</h3>

<h4>First of all got to Devices -> Insert Guest Additions CD image<h4>
<img src="images/Screenshot_11.png" width="800" height="600">

<h3>From the terminal, run the following commands:<h3>

```sh
sudo su
apt install gcc make
mkdir --parents /media/cdrom
mount /dev/cdrom /media/cdrom
/media/cdrom/VBoxLinuxAdditions.run
reboot
```

# Disable Swap

```sh
sudo sed -i '/\sswap\s/s/^/#/' /etc/fstab
sudo swapoff -a
free -h
```
<h3>Should look like this</h3>
<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*XFIwxWHc9SMMXMcWb65-GQ.png" width="900" height="50">

# Install kubernetes
<h3>Now it’s time to install kubernetes itself on the master node. I made my cluster set up for 1.25.4 version</h3>
<h3>I’m going to put all required commands to k8s.sh file to run it in master node, and worker nodes after all</h3>

```sh
# k8s.sh
sudo apt-get update
sudo apt install curl apt-transport-https -y
curl -fsSL  https://packages.cloud.google.com/apt/doc/apt-key.gpg|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/k8s.gpg
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update
sudo apt install kubelet=1.25.4-00 kubeadm=1.25.4-00 kubectl=1.25.4-00 -y
sudo apt-mark hold kubelet kubeadm kubectl
```
# Check your installation

```sh
kubectl version --output=yaml
kubeadm version --output=yaml
```
# Install docker

<h3>I’m going to use Docker as a container runtime for kubernetes in my cluster</h3>
<h3>To make in complaint with kubernetes I will use Mirantis. It’s an adapter for Docker Engine to implement CRI interfaces</h3>

```sh
#docker.sh
sudo apt update
sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y containerd.io docker-ce docker-ce-cli

sudo mkdir -p /etc/systemd/system/docker.service.d

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

