+++
title = "Create a new Kubernetes cluster"
description = ""
weight=40
+++
{{%excerpt%}}
To create a new Kubernetes cluster from scratch using Nirmata follow the
steps below. With this option, Kubernetes cluster will be deployed on an
existing host group.

Configure firewall/security groups

Please ensure that the following ports are open in the host group:

TCP: 6443, 8080 (from master only), 2379 (for etcd), 12050 (all hosts)
UDP: 4789 (VXLAN) ICMP on all ports

Create a Managed Kubernetes Cluster:

1.  Go to the Clusters panel and click on the Add Cluster button.
2.  Select: No - Install and manage Kubernetes for me
 ![image](/images/create-kubernetes-cluster-ins-1.png)
3. Provide the cluster name and add host groups that you would like to
install the cluster on. Also select the cluster policy. Other fields are
optional. Click on Create cluster and start the installation button to
proceed with the cluster install.
 ![image](/images/create-kubernetes-cluster-ins-2.png)
4.  Within a few minutes, the cluster will be deployed, the Nirmata
    controller should connect and the cluster state will show as
    Connected.
 ![image](/images/create-kubernetes-cluster-ins-3.png)

Once the cluster is deployed and in Ready state, you can create
Environments for this cluster to deploy your applications.
{{%/excerpt%}}
