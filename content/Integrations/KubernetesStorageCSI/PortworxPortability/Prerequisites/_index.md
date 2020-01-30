+++
title = "Prerequisites"
description = ""
weight=20
+++
{{%excerpt%}}
#### Key-Value Store
Portworx uses a key-value store for clustering metadata. This integration example utilizes the default etcd.

#### Storage
Ensure that at least one of the Portworx nodes has extra storage available. Use an unformatted partition or a disk-drive.

Storage devices explicitly given to Portworx are automatically formatted by Portworx. Before integrating Nirmata with Portworx, add an unused disk on each worker node of the same size and confirm that the mount point is /dev/sd*).

#### Shared Mounts
If running Docker v1.12, Docker must be configured to allow shared mounts propagation. If not, Portworx will fail to start.

[Click here for instructions on configuring Docker v1.12 to allow shared mounts propagation](https://docs.portworx.com/knowledgebase/shared-mount-propagation.html).

#### Firewall
Ensure that ports 9001-9015 are open between the nodes that will run Portworx.

#### NTP
Ensure that all nodes running Portworx are time-synchronized and that an NTP service is configured and running.

{{%/excerpt%}}