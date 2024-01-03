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

<h3>In the command above pay attention that I chose subnet 10.244.0.0/16 for kubernetes cluster nodes, so pods will be communicating between each other using this subnet inside cluster.</h3>

<h3>Installation may take some time and you can check master-vm.log file.</h3>

```sh
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of the control-plane node running the following command on each as root:

  kubeadm join master-vm:6443 --token e8r3yb.it74vseuaxlzjlzp \
 --discovery-token-ca-cert-hash sha256:a43e08f52250a63486dd373cd50756a2ac0e90b62fbf0031a5e386f3d7e4f816 \
 --control-plane --certificate-key 308b550f6f9de654510db8b24cae39996727f70097ec8b9736a793a45573a7ed

Please note that the certificate-key gives access to cluster sensitive data, keep it secret!
As a safeguard, uploaded-certs will be deleted in two hours; If necessary, you can use
"kubeadm init phase upload-certs --upload-certs" to reload certs afterward.

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join master-vm:6443 --token e8r3yb.it74vseuaxlzjlzp \
 --discovery-token-ca-cert-hash sha256:a43e08f52250a63486dd373cd50756a2ac0e90b62fbf0031a5e386f3d7e4f816
```

<h3>Don’t forget to copy /etc/kubernetes/admin.conf to your home directory and to home directory on your master node as described in master-vm.log</h3>

```sh
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
<h3>To copy /etc/kubernetes/admin.conf to your local computer you can use shared directory.</h3>

# Configure Kubernetes cluster network.
<h3>For communication between different nodes in cluster another CNI plugin is required. I chose Flannel for my cluster.</h3>

```sh
wget https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml

```
<h3>In kube-flannel.yml check net-conf.json “Network” tag. It should have the same value as was used during control plane setup, i.e. 10.244.0.0/16.</h3>

```sh
#kube-flannel.yaml
cat kube-flannel.yaml

  net-conf.json: |
    {
      "Network": "10.244.0.0/16",
      "Backend": {
        "Type": "vxlan"
      }
    }
```

<h3>Finally, execute kubectl command</h3>

```sh
kubectl apply -f kube-flannel.yml
```
<h3>If you need to reinstall Flannel use kubectl delete</h3>

```sh
kubectl delete -f kube-flannel.yml
```

<h3>Flanneld config is created in /etc/cni/net.d/10-flannel.conflist.
When starting Flanneld extracts cluster network config in file /run/flannel/subnet.env.</h3>

```sh
#/run/flannel/subnet.env
FLANNEL_NETWORK=10.244.0.0/16
FLANNEL_SUBNET=10.244.1.1/24
FLANNEL_MTU=1450
FLANNEL_IPMASQ=true
```

<h3>Flannel pods are created in its own namespace kube-flannel, so you can check flannel pods are running</h3>>

```sh
kubectl get pods -n kube-flannel
```

# Joining worker nodes

<h3>As soon as Flannel installed, everything is ready to join worker nodes to cluster to finish setup.
In log file of kubeadm init command (master-vm.log) there is already a join command to use to join worker node to cluster.</h3>

<h2>kubeadm join requires a special token. It expires in 24 hours</h2>
to generate join command

```sh
kubeadm token create --print-join-command
```
<h3>Now you can connect to your worker nodes and join the cluster.
Do not forget to add IP mapping for master-vm in /etc/hosts on all you worker nodes
! We will have to append this line to the join procces --cri-socket unix:///var/run/cri-dockerd.sock
</h3>


```sh
kubeadm join k8smaster:6443 --token e8r3yb.it74vseuaxlzjlzp \
--discovery-token-ca-cert-hash sha256:a43e08f52250a63486dd373cd50756a2ac0e90b62fbf0031a5e386f3d7e4f816 --cri-socket unix:///var/run/cri-dockerd.sock
```
