+++
title = "Google Kubernetes Engine (GKE)"
description = ""
weight=10
+++
{{%excerpt%}}
#### Feature Overview

The Cloud Provider Cluster Support features enable users to create,  upgrade, resize, and delete a Google Kubernetes Cluster (GKE) from within Nirmata.

#### How to Manage a GKE Cluster in Nirmata

To manage a GKE Cluster in Nirmata, add Google as a Cloud Provider in Nirmata. A valid Google Cloud Provider account and credentials is required.

See [GCE Cloud Provider](https://docs.nirmata.io/cloudproviders/gce_cloud_provider/) for full documentation on adding Google as a Cloud Provider.

#### Create a GKE Cluster

To add a GKE Cluster in Nirmata, select Clusters from the sidebar menu and then click the *+Add Cluster* button.

![image](/images/gke-1.png)

Select *Create GKE Cluster* and click *Complete Setup*.

![image](/images/gke-2.png)

Enter the *Configure Cluster Details* and click *Next*.

![image](/images/gke-3.png)

Complete the *Configure Cluster Details* and click *Create Cluster*.

![image](/images/gke-4.png)

The Cluster will begin building.

![image](/images/gke-5.png)

In 10 to 15 minutes, the new Cluster is visible in Nirmata and in the Google Cloud Provider dashboard.

![image](/images/gke-6.png)

![image](/images/gke-7.png)

#### Upgrade a GKE Cluster

NOTE: The Kubernetes version associated with a cluster **cannot** be downgraded.
To upgrade the Kubernetes version of a GKE Cluster, navigate to the cluster from the Cluster menu.

![image](/images/gke-8.png)

Select *Upgrade Cluster*  from the *Settings* menu.

![image](/images/gke-9.png)

Select the new Kubernetes version from the drop-down menu and click *Save*.

![image](/images/gke-10.png)

The upgrade is reflected in Google Cloud Platform and Nirmata.

![image](/images/gke-11.png)

![image](/images/gke-12.png)

#### Resize a GKE Cluster

To change the number of nodes in a GKE Cluster, navigate to the cluster from the *Cluster* menu.

![image](/images/gke-13.png)

Open the *Settings* menu and select *Resize Cluster*.

![image](/images/gke-14.png)

Enter the new node count and click *Save*.

![image](/images/gke-15.png)

The new nodes are reflected on the Nirmata Cluster dashboard.

![image](/images/gke-16.png)

#### Delete a GKE Cluster

NOTE: All Applications and Environments running inside the cluster must be stopped and deleted before deleting the cluster.

To delete a GKE Cluster, navigate to the cluster from the *Cluster* menu.

![image](/images/gke-17.png)

From the *Settings* menu, select *Delete Cluster*.

![image](/images/gke-18.png)

Enter the Cluster name and click Delete.

![image](/images/gke-19.png)

The cluster is deleted in Nirmata and Google Cloud Platform.

![image](/images/gke-20.png)
![image](/images/gke-21.png)

{{%/excerpt%}}
