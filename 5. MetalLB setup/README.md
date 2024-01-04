# Metallb Setup

<img src="/img/metallb-icon-color.png" width="180" height="180">

# Set up a MetalLB Load Balancer on a on-premises Kubernetes Cluster

Without MetalLB or any similar software solution the External IP of any new created service in Kubernetes will stay indefinitely in pending state. MetalLB’s purpose is to cover this deficit by offering a network load balancer implementation that integrates with standard network equipment, so that external services on bare-metal clusters work in a similar way as their equivalents in IaaS platform providers.

# Installation
The installation of MetalLB is easy we are going to perform it by applying the necessary manifests (everything will be provisioned in a new namespace named metallb-system)
