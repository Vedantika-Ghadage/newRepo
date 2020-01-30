+++
title = "Application Portability Steps"
description = ""
weight=100
+++
{{%excerpt%}}

The use case for application portability between Nirmata and Portworx requires the following:

1. Demonstrate an application created in a shared Nirmata environment (namespace) tied to an infrastructure (private cloud) using dynamically provisioned PVCs for a sample application (MySQL).
2. Demonstrate single-click application migration using Nirmata *clone application button*.
3. This action triggers migration of application YAML to a different environment tied to different infrastructure (public cloud) with an associated namespace.
4. On the storage side, this triggers a backup of associated PVCs and volumes to an S3 object-store in the destination cloud.
5. The logic recreates persistent volumes.
6. The application clone logic statically configures the PVCs and PVs based on data from the application deployed in the first cluster.

{{%/excerpt%}}