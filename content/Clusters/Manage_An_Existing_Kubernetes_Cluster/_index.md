+++
title = "Manage an Existing Kubernetes Cluster"
description = ""
weight=30
+++
{{%excerpt%}}
To manage an existing Kubernetes cluster with Nirmata

1.  Go to the Clusters panel and click on the Add Cluster button.
2.  Select: "Yes - I have already installed Kubernetes"
 ![image](/images/create-kubernetes-cluster-2.png)
3.  Provide the cluster name and select the provider for your cluster.
    Leave the provider as Other in case your cluster provider is not in
    the list.
 ![image](/images/create-kuberenetes-cluster-disc-1.png)
4.  Follow the displayed instructions to install the Nirmata Kubernetes
    controller and click on button confirming the installation.
 ![image](/images/create-kuberenetes-cluster-disc-2.png)
5.  Within a few seconds, the controller should connect and the cluster
    state will show as Connected.
 ![image](/images/create-kuberenetes-cluster-disc-3.png)
Once the cluster is in Ready state, you can deploy Applications to this
cluster.

**Note:** Only Kubernetes versions 1.8.6 and above are currently supported.
{{%/excerpt%}}
