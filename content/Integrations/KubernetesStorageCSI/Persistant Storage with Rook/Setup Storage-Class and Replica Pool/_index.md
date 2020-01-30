+++
title = "Setup Storage Class and Replica Pool"
description = ""
weight=50
+++
{{%excerpt%}}

To setup a storage-class and replica pool, import the storage-class for block storage. 

**Storage-Class for Block Storage YAML:**  

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
   name: rook-ceph-block
provisioner: ceph.rook.io/block
parameters:
  pool: replicapool
  # Specify the namespace of the rook cluster from which to create volumes.
  # If not specified, it will use `rook` as the default namespace of the cluster.
  # This is also the namespace where the cluster will be
  clusterNamespace: rook-ceph
  # Specify the filesystem type of the volume. If not specified, it will use `ext4`.
#  fstype: xfs
```
Apply storage-class for block storage to the Kubernetes Cluster using the *Apply YAML* option in the Cluster Settings menu. 

![image](/images/rook-17.png)

Drop the storage-class.yaml file into the upload  box or select the file from the directory. 

![image](/images/rook-18.png)

Next, import the replica-pool setting manifest into the Kubernetes Cluster in the rook-ceph Environment. 

**Replica-Pool YAML Manifest:**
```
apiVersion: ceph.rook.io/v1beta1
kind: Pool
metadata:
  name: replicapool
  namespace: rook-ceph
spec:
  failureDomain: host
  replicated:
    size: 2 
```

To import the replica-pool setting manifest, click the gear in the top right corner of the Running Application window and select the *Import to Application* option. 

![image](/images/rook-19.png)

Drop the Replica-Pool YAML Manifest file into the upload  box or select the file from the directory. 

![image](/images/rook-20.png)

Verify that storage-class is configured on the cluster through the Nirmata shell. 

![image](/images/rook-21.png)

Verify that the pool is set to a replication size of 2. 

![image](/images/rook-22.png)


   
{{%/excerpt%}}