+++
title = "Azure Kubernetes Service (AKS)"
description = ""
weight=30
+++
{{%excerpt%}}
#### Feature Overview

The Cloud Provider Cluster Support features enable users to create,  upgrade, resize, and delete a new Microsoft Azure (AKS) cluster in Nirmata.

NOTE: The Kubernetes version associated with a cluster **cannot** be downgraded.

#### How to Manage an AKS Cluster in Nirmata

To manage an AKS Cluster in Nirmata, add Azure as a Cloud Provider in Nirmata. A valid Microsoft Azure account and credentials is required.

See [Microsoft Azure Cloud Provider](https://docs.nirmata.io/cloudproviders/microsoft_azure_cloud_provider/) for full documentation on adding Azure as a Cloud Provider.

#### Create an AKS Cluster

To add an AKS Cluster in Nirmata, select Clusters from the sidebar menu and then click the *+Add Cluster* button.

![image](/images/aks-1.png)

Select *Create AKS Cluster* and click *Complete Setup*.

![image](/images/aks-2.png)

Enter the *Configure Cluster Details* and click *Next*.

![image](/images/aks-3.png)

Select the *VMSize Type* and *Node Count*.

NOTE:	Maximum node counts apply to each VMSize type.

![image](/images/aks-4.png)

![image](/images/aks-5.png)

View the new cluster in AKS by navigating from the AKS Home screen to *Kubernetes Services*. 
The new cluster is displayed.

![image](/images/aks-6.png)

Click on the cluster name to view the cluster details in AKS. In 15 to 20 minutes, the cluster will complete the *Creating* process and will be available for configuration in AKS and Nirmata.

![image](/images/aks-7.png)

#### Upgrade an AKS Cluster

NOTE: The Kubernetes version associated with a cluster **cannot** be downgraded.
To upgrade the Kubernetes version of an AKS Cluster, navigate to the cluster from the Cluster menu.

![image](/images/aks-8.png)

Select *Upgrade Cluster* from the *Settings* menu.

![image](/images/aks-9.png)

Select the new Kubernetes version from the drop-down menu and click *Save*.

![image](/images/aks-0.png)

The upgrade is reflected in AKS and Nirmata.

![image](/images/aks-10.png)

![image](/images/aks-11.png)

#### Resize an AKS Cluster

To change the number of nodes in a AKS Cluster, navigate to the cluster from the Cluster menu.

![image](/images/aks-12.png)

Open the *Settings* menu and select *Resize Cluster*.

![image](/images/aks-13.png)

Enter the new node count and click *Save*.

![image](/images/aks-14.png)

The new nodes are reflected on the Nirmata Cluster dashboard.

![image](/images/aks-15.png)

#### Delete an AKS Cluster

NOTE: All Applications and Environments running inside the cluster must be stopped and deleted before deleting the cluster.

To delete an AKS Cluster, navigate to the cluster from the *Cluster* menu.

![image](/images/aks-16.png)

From the Settings menu, select *Delete Cluster*.

![image](/images/aks-17.png)

Enter the Cluster name and click *Delete*.

![image](/images/aks-18.png)

The cluster is deleted in Nirmata and AKS.

![image](/images/aks-19.png)

![image](/images/aks-20.png)


{{%/excerpt%}}
