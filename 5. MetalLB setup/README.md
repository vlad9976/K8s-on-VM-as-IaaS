# Metallb Setup

<img src="/img/metallb-icon-color.png" width="180" height="180">

# Set up a MetalLB Load Balancer on a on-premises Kubernetes Cluster

Without MetalLB or any similar software solution the External IP of any new created service in Kubernetes will stay indefinitely in pending state. MetalLB’s purpose is to cover this deficit by offering a network load balancer implementation that integrates with standard network equipment, so that external services on bare-metal clusters work in a similar way as their equivalents in IaaS platform providers.

# Example Try:

```sh
kubectl create deployment nginx-server --image=nginx
kubectl expose deployment nginx-server --type LoadBalancer --port 80 --target-port 8080
```
# output
<img src="/images/Screenshot_3.png" width="180" height="180">

# Installation
The installation of MetalLB is easy we are going to perform it by applying the necessary manifests (everything will be provisioned in a new namespace named metallb-system)


```sh
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.7/config/manifests/metallb-native.yaml
```
we need to provide the components required by MetalLB. The next manifest will deploy MetalLB to the cluster, in metallb-system namespace we just created. The components are:

```sh
1. the metallb-system/controller deployment. A cluster-wide controller that handles IP assignments.
2. the metallb-system/speaker which is a daemonset. That is the component to make the services reachable.
3. the service accounts for the controller and speaker, along with the RBAC permissions that the components require.
```
