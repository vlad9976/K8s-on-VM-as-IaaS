# <img src="/img/icons8-cluster-64.png" width="40" height="40"> Create Kubernetes cluster.

<h4>If you finished successfully all previous steps you should have 3 virtual machines with Ubuntu, kubernetes and docker installed.</h4>
<h4>For cluster creation kubeadm command is used. First, it pulls images for kubernetes control plane to container runtime (docker in our case) and then initializes the control plane.<h4>

<h4>1. Control plane will be created on master node, and worker nodes will be joined after all.</h4>

```sh
sudo kubeadm config images pull --cri-socket /run/cri-dockerd.sock
```

<h4>2. Check /etc/hosts on master node. It should contain mapping for master-vm</h4>
<h4>DONT forget to map Workers to /etc/hosts on the master </h4>

```sh
cat /etc/hosts
```

# <h4>3.  Start init command</h4>

```sh
sudo kubeadm init \
  --pod-network-cidr=10.244.0.0/16 \
  --cri-socket /run/cri-dockerd.sock  \
  --upload-certs \
  --control-plane-endpoint=master-vm:6443 >  master-vm.log
```

<h4>In the command above pay attention that I chose subnet 10.244.0.0/16 for kubernetes cluster nodes, so pods will be communicating between each other using this subnet inside cluster.</h4>

<h4>Installation may take some time and you can check master-vm.log file.</h4>

```sh
# cat master-vm.log
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

<h4>4. Don’t forget to copy /etc/kubernetes/admin.conf to your home directory and to home directory on your master node as described in master-vm.log</h4>

```sh
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
<h4>To copy /etc/kubernetes/admin.conf to your local computer you can use shared directory.</h4>

# <h4>5. <img src="../img/icons8-network-65.png" width="40" height="40"> Configure Kubernetes cluster network.</h4>

<h4>For communication between different nodes in cluster another CNI plugin is required. I chose Flannel for my cluster.</h4>

<img src="/img/flannel.svg" width="30" height="30"> Flannel git page: https://github.com/flannel-io/flannel

```sh
wget https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml

```
<h4>In kube-flannel.yml check net-conf.json “Network” tag. It should have the same value as was used during control plane setup, i.e. 10.244.0.0/16.</h4>

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

<h4>6. Finally, execute kubectl command</h4>

```sh
kubectl apply -f kube-flannel.yml
```
<h4>If you need to reinstall Flannel use kubectl delete</h4>

```sh
kubectl delete -f kube-flannel.yml
```

<h4>Flanneld config is created in /etc/cni/net.d/10-flannel.conflist.
When starting Flanneld extracts cluster network config in file /run/flannel/subnet.env.</h4>

```sh
#/run/flannel/subnet.env
FLANNEL_NETWORK=10.244.0.0/16
FLANNEL_SUBNET=10.244.1.1/24
FLANNEL_MTU=1450
FLANNEL_IPMASQ=true
```

<h4>Flannel pods are created in its own namespace kube-flannel, so you can check flannel pods are running</h4>

```sh
kubectl get pods -n kube-flannel
```

# Joining worker nodes 👾

<h4>As soon as Flannel installed, everything is ready to join worker nodes to cluster to finish setup.
In log file of kubeadm init command (master-vm.log) there is already a join command to use to join worker node to cluster.</h4>

<h2>kubeadm join requires a special token <img src="/img/icons8-access-64.png" width="30" height="30"> . It expires in 24 hours</h2>
To generate new token on master use:

```sh
kubeadm token create --print-join-command
```
<h4>Now you can connect to your worker nodes and join the cluster <img src="../img/icons8-add-node-96.png" width="40" height="40"></h4>
  
<h4>Do not forget to add IP mapping for master-vm in /etc/hosts on all worker nodes</h4>

<h4>7. We will have to append this line to the join command --cri-socket unix:///var/run/cri-dockerd.sock</h4>


```sh
kubeadm join k8smaster:6443 --token e8r3yb.it74vseuaxlzjlzp \
--discovery-token-ca-cert-hash sha256:a43e08f52250a63486dd373cd50756a2ac0e90b62fbf0031a5e386f3d7e4f816 --cri-socket unix:///var/run/cri-dockerd.sock
```

<h2>Wait for a while and you can check the installation using kubectl</h2>

```sh
kubectl get node
or
kubectl get node -o wide
```
# <h4>✅ Check cluster setup</h4>
<h4>By default kubernetes uses default namespace. For system pods it uses kube-system, flannel uses kube-flannel. To get all pods from all namespaces you can use</h4>

```sh
kubectl get pod --all-namespaces
# Output
NAMESPACE       NAME                                        READY   STATUS    RESTARTS      AGE
kube-flannel    kube-flannel-ds-7nhwn                       1/1     Running   0              5m
kube-flannel    kube-flannel-ds-sxfgg                       1/1     Running   0             10m
kube-flannel    kube-flannel-ds-xxhlh                       1/1     Running   0             12m
kube-system     coredns-565d847f94-9ht74                    1/1     Running   0             17m
kube-system     coredns-565d847f94-wrq24                    1/1     Running   0             17m
kube-system     etcd-k8smaster                              1/1     Running   0             17m
kube-system     kube-apiserver-k8smaster                    1/1     Running   0             17m
kube-system     kube-controller-manager-k8smaster           1/1     Running   0             17m
kube-system     kube-proxy-9nfd4                            1/1     Running   0             17m
kube-system     kube-proxy-cf7v7                            1/1     Running   0              5m
kube-system     kube-proxy-cmq2k                            1/1     Running   0             10m
kube-system     kube-scheduler-k8smaster                    1/1     Running   0             12m
```
<h4>Pay attention that there are 3 flannel pods, each for every node.
All pods should running fine.</h4>

<h4>If you have some errors you can get details using</h4>

```sh
kubectl describe pod kube-flannel-ds-7nhwn -n kube-flannel
kubectl logs kube-flannel-ds-7nhwn -n kube-flannel
```

 [<img src="../img/icons8-next-96.png" width="75" height="75"> <img src="../img/metallb-icon-color.png" width="75" height="75">][PlDa]
 
 [PlDa]:<../5. MetalLB setup/README.md>

