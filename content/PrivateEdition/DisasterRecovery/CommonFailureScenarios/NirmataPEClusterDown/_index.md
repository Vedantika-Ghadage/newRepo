+++
title = "Nirmata PE Cluster is Down"
description = ""
weight=10
+++
{{%excerpt%}}

#### Failure Impact of a Down Nirmata PE Cluster

When a Nirmata PE cluster loses service the Kubernetes cluster may not go down.

Nirmata PE manages Kubernetes clusters through an API. Since the Nirmata PE cluster is deployed in a separate node from Kubernetes cluster, the Kubernetes cluster only goes down when the entire Pod or rack system goes down.

Unless this happens, it is likely that the Kubernetes cluster will maintain service and operation, which means minimal impact to applications.

Nirmata PE has a microservices based architecture and is built as a set of container services. This ensures that when a component goes down it comes right back up. 

In HA configuration, a Nirmata PE cluster will go down only when all three nodes that form the cluster go down.

If  a specific component goes down, the Kubernetes cluster recreates the down pd and the service.

#### How to Perform a Backup When the Nirmata PE Cluster is Down

To prepare Nirmata PE for recovery, start by backing-up and securing essential Nirmata PE installation configuration and state data. 

Backup the following key components:  

1. Nirmata PE certificates
2. Nirmata PE installation configuration
3. Nirmata PE state - which is stored in the MongoDB database as part of shared services in Nirmata PE

Use the following process to backup the key components described:

1. As a best practice, store certificate files in the installer directory and backup the original certificate files. These files are required to recover Nirmata PE in the correct configuration and will be  restored in the new installer directory.
2. Configuration information is stored in the nirmata.conf file in the installer directory. Create a backup of this file.
3. Nirmata PE utilizes its own CLI command to perform routine backups of the database. Use the Nirmata PE CLI Backup Command as part of a cronjob to force a backup.

**Nirmata PE CLI Backup Command:**

```
nadm backup -n <install-namespace> -d <backup-dir>
```

#### How to Recover from a Nirmata PE Cluster Failure

After performing the backup steps described, complete the following service recovery steps:

1. Restore the backed-up files and certificates in the installer directory.
2. Install a new instance of Nirmata.
3. Run the Nirmata PE Restore CLI Command to restore the database with th state information of the down cluster.

**Nirmata PE Restore CLI Command:**

```
nadm restore
```

{{%/excerpt%}}
