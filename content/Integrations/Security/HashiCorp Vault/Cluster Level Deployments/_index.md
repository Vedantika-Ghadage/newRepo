+++
title = "Cluster Level Deployments"
description = ""
weight=50
+++
{{%excerpt%}}

To deploy Vault at the cluster level, begin by deploying CRDs.

[Deploy the etcd_crds.yaml](https://github.com/coreos/vault-operator/blob/master/example/etcd_crds.yaml)
[Deploy the vault_crd.yaml](https://github.com/coreos/vault-operator/blob/master/example/vault_crd.yaml)

To deploy a YAML on a cluster, open the cluster and then select *Apply YAML* from the Cluster Settings menu.

![image](/images/vault-2.png)

Drop the YAML file into the upload  box or select the file from the directory.

{{%excerpt%}}