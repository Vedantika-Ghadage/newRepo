+++
title = "How to Deploy the Vault Cluster"
description = ""
weight=70
+++

{{%excerpt%}}

To deploy the Vault cluster, create a new application. Click on *Catalog* in the sidebar menu and then select *Application Catalog*. From the main Application Catalog screen, click *Add Application*.

Add the sample Vault Cluster YAML file.

**Sample Vault Cluster YAML:**

```
apiVersion: "vault.security.coreos.com/v1alpha1"
kind: "VaultService"
metadata:
  name: "example"
spec:
  nodes: 2
  version: "0.9.1-0"
```

![image](/images/vault-9.png)

Run Sample Vault Cluster application in the Vault environment, open the environment and click *+Run Application*.

![image](/images/vault-10.png)

After deploying the Sample Vault Cluster, the cluster will display:

```
kubectl -n default get pods -l app=vault,vault_cluster=example
```

_Note:_ Cluster value and namespace value are environment-dependent.

As the Vault cluster comes online, various pods will begin starting up and running.

{{%excerpt%}}