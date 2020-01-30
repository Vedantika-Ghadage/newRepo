+++
title = "Prerequisites"
description = ""
weight=20
+++
{{%excerpt%}}

1. Nirmata Cluster with Kubernetes 1.10+, minimum 1 node in a cluster ( We are using Kubernetes version 1.10.8 with 6 nodes). 
2. Nutanix CE version 5.5 and later  
3. iSCSI OS plugin  
••1. Centos: iscsi-initiator-utils  
••2. Ubuntu: open-iscsi  
••3. All worker nodes must have the same iSCSI initiator in /etc/iscsi/initiatorname.iscsi

{{%excerpt%}}