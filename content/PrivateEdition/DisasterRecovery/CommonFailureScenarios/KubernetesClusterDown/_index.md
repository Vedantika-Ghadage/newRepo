+++
title = "Kubernetes Cluster is Down"
description = ""
weight=20
+++
{{%excerpt%}}

#### Failure Impact of a Down Kubernetes Cluster

If a Kubernetes cluster is installed in a High Availability configuration, the Kubernetes cluster will continue to operate until the last master node goes down.

Even when the master node goes down, worker nodes may continue to operate and run the containers orchestrated on those nodes. If certain applications or pods were running on those master nodes, those applications and pods will go down. However, if another master node exists, Kubernetes will look to recreate those pods on other available nodes.

Recovering from a master node failure is more complex than recovering from a worker node failure. However, master node failure does not mean that the cluster and all workloads are lost.

The cluster and all workloads will continue running with exactly the same configuration as before the failure. Applications running in the Kubernetes cluster will still be usable. However, it is not possible to create new deployments or to recover from node failures without the master node.

#### How to Perform a Backup When a Kubernetes Cluster is Down

There are several components required to recover a master node on a Kubernetes cluster:

1. Certificates
2. Secrets
3. etcd Database
4. Persistent Volumes (stateful containers only)

#### How to Recover from a Kubernetes Cluster Failure

Currently, Kubernetes has the latest release 1.12 with snapshot and recovery capability in beta. 

Nirmata PE will support these features for backup and restore capability as they become generally available. Until snapshot recovery is available, Nirmata recommends using [kubeadm](https://labs.consol.de/kubernetes/2018/05/25/kubeadm-backup.html) to recover.