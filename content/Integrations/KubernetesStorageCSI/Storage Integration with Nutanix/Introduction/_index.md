+++
title = "Introduction"
description = ""
weight=10
+++
{{%excerpt%}}

Nutanix provides an external volume plug-in for Kubernetes. Kubernetes is an open source platform for automating deployment, scaling, and operation of application containers across a cluster of hosts. This cluster of hosts can be made up of cloud provider VM instances, Nutanix-hosted VMs, or bare metal servers. A Kubernetes cluster is formed with multiple nodes, and must contain at least one master node.

This plug-in runs in a pod and dynamically provisions requested persistent volume that is compatible with the Kubernetes iSCSI volume. Nutanix then provides persistent storage for the provisioned volume.

Storage classes also have provisioners which determine which volume plugin should be used for provisioning Persistent Volumes.
Read more about Nutanix with Kubernetes (here)[https://portal.nutanix.com/#/page/docs/details?targetId=Kubernetes-Volume-Plug-In-v10:Kubernetes-Volume-Plug-In-v10].
   
{{%/excerpt%}}