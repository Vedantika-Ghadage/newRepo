+++
title = "More Nirmata Setup Help"
description = ""
weight= 30
+++
{{%excerpt%}}

#### More Nirmata Setup Help

[Setup vSphere Private Cloud-Provider](https://docs.nirmata.io/cloudproviders/)

[Setup a vSphere private-cloud provider](https://docs.nirmata.io/cloudproviders/vmware_vsphere_cloud_provider/)

[Setup vSphere Host-Group](https://docs.nirmata.io/hostgroups/vmware_vsphere_host_group/)

[Setup Nodes and Load-Balancer for HA configuration](https://docs.nirmata.io/clusters/high_availability_ha_clusters/)

[Configure Storage-Class for vSphere Cluster Policy](https://docs.nirmata.io/clusters/cluster_policies/)

[Configure Kubernetes Cluster on vSphere](https://docs.nirmata.io/clusters/create_a_new_kubernetes_cluster/)

**Add Storage Class Template:**

```
metadata:
  name: filesystem
  selfLink: /apis/storage.k8s.io/v1/storageclasses/filesystem
  labels:
    nirmata.io/storageclass.name: filesystem
provisioner: kubernetes.io/vsphere-volume
apiVersion: storage.k8s.io/v1
reclaimPolicy: Retain
kind: StorageClass
parameters:
  diskformat: thin
  ```
