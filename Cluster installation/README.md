# Create Kubernetes cluster.

<h3>If you finished successfully all previous steps you should have 3 virtual machines with Ubuntu, kubernetes and docker installed.</h3>
<h3>For cluster creation kubeadm command is used. First, it pulls images for kubernetes control plane to container runtime (docker in our case) and then initializes the control plane.<h3>

<h3>Control plane will be created on master node, and worker nodes will be joined after all.</h3>