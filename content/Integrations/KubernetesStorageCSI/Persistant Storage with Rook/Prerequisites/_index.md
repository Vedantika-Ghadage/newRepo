+++
title = "Prerequisites"
description = ""
weight=20
+++
{{%excerpt%}}

1. Nirmata Cluster with Kubernetes 1.7+, minimum 3 nodes in a cluster. The example that follows uses Kubernetes version 1.9.4 with 4 nodes.
2. Flex Volume Configuration: Enabled by default with Nirmata
 (Directory: "/opt/nirmata/volume-plugins")
3. kubectl: 1.9+ (for setting rook cluster)
4. dataDirHostPath Storage: Path on VM node(host) to store config and data for rook services (enough to meet container persistent storage requirements); default is /var/lib/rook
5. Linux packages: rbd-fuse, ceph-fs-common
   
{{%/excerpt%}}