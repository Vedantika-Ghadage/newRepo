+++
title = "Persistent Volume Claims"
description = ""
weight=40
+++
{{%excerpt%}}
A PersistentVolumeClaim (PVC) is a request for storage for a pod. PVCs
are used to create Persistent Volumes (PV) for your pods). PVCs can
request specific size and access modes for storage.

*Tip:* When creating a StatefulSet, you can create VolumeClaimTemplates
instead of using PVCs. This will allow you to scale your StatefulSet.
{{%/excerpt%}}
