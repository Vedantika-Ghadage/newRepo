+++
title = "Deploying Vault in a Nirmata Kubernetes Cluster"
description = ""
weight=30
+++
{{%excerpt%}}

Integrating Nirmata with Vault begins with deploying Vault Operator in the cluster.

To deploy Vault Operator in a cluster, [create and configure a Kubernetes cluster through Nirmata.](https://docs.nirmata.io/clusters/)

Next, pull the Vault specific binaries, configuration, and YAML files. Then configure the necessary (RBAC policy.](https://github.com/coreos/vault-operator/blob/master/example/rbac-template.yaml

After configuring the RBAC policy, [deploy Flannel. ](https://docs.nirmata.io/clusters/cluster_policies/)

Vault Operator uses an [etcd operator](https://github.com/coreos/etcd-operator/) as backend storage. Create and deploy custom resource definitions (CRD) to an etcd operator and then create and deploy a Vault cluster with the custom resource definitions.

{{%excerpt%}}