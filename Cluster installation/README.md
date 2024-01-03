# Create Kubernetes cluster.

<h3>If you finished successfully all previous steps you should have 3 virtual machines with Ubuntu, kubernetes and docker installed.</h3>
<h3>For cluster creation kubeadm command is used. First, it pulls images for kubernetes control plane to container runtime (docker in our case) and then initializes the control plane.<h3>

<h3>Control plane will be created on master node, and worker nodes will be joined after all.</h3>

```sh
sudo kubeadm config images pull --cri-socket /run/cri-dockerd.sock
```

<h3>Check /etc/hosts on master node. It should contain mapping for master-vm</h3>

```sh
cat /etc/hosts
```

# Start init command

```sh
sudo kubeadm init \
  --pod-network-cidr=10.244.0.0/16 \
  --cri-socket /run/cri-dockerd.sock  \
  --upload-certs \
  --control-plane-endpoint=master-vm:6443 >  master-vm.log
```