<a href="https://kubernetes.io/" target="_blank"><img style="margin: 10px" src="https://profilinator.rishav.dev/skills-assets/kubernetes-icon.svg" alt="Kubernetes" height="180" /></a> 
<img src="/img/metallb-icon-color.png" width="180" height="180">
<img src="/img/icons8-nginx-accelerates-content-and-application-delivery-improves-security-96.png" width="180" height="180">
<img src="/img/icons8-virtualbox-logo-96.png" width="180" height="180">
<br>
<h3>Kubernetes bare-metal clusters work in a similar way as their equivalents in IaaS platform providers🚀(Virtualbox📦)</h3>
<h4>😅 Why K8s? Because between the K and the S there are 8 letters.</h4>
<h4>We will create kubernetes cluster on Ubuntu Server 22.04 LTS<br>Using virtualbox and deploying Metallb Loadbalancer and Nginx ingress controller</h4>

<h3>To Start read Down <img src="/img/icons8-down-96.png" width="30" height="30"></h3>

# <h3>Steps in short</h3>
1. Spin 3 Virtual machines<br>
   1.1 Master 🤖<br>
   1.2 Worker 👾👾
3. Install Kubernetes cluster 1.25.4 version🕸️ <br>
   2.1 Install kubelet 1.25.4-00 🚤<br>
   2.2 Insatll kubectl 1.25.4-00 🏗️</br>
   2.3 Install kubeadm 1.25.4-00 🏭
   
3. Install docker🐋<br>
   3.1 Install CRI(Container Runtime)<br>
   3.2 Install Mirantis
   
4. Create Kubernetes cluster <br>
   4.1 Config image pull cri-dockerd.sock ⬇️<br>
   4.2 Init kubernetes cluster ♾️<br>

5. Join worker nodes 🔌<br>

6. Deploy Metallb

7. Deploy Nginx ingress

# Requirments
VirtualBox📦

[<img src="/img/icons8-start-40.png" width="50" height="50">][PlDa]
 
[PlDa]:<./1. Virtual Machines/README.md>




