+++
title = "Add Custom Resource Definitions"
description = ""
weight=60
+++

{{%excerpt%}}

To deploy Vault at the cluster level, begin by deploying CRDs.

Deploy the [etcd_crds.yaml](https://github.com/coreos/vault-operator/blob/master/example/etcd_crds.yaml)
Deploy the [vault_crd.yaml](https://github.com/coreos/vault-operator/blob/master/example/vault_crd.yaml)

To deploy a YAML on a cluster, open the cluster and then select Apply YAML from the Cluster Settings menu.

![image](/images/vault-2.png)

Drop the YAML file into the upload  box or select the file from the directory. 

#### Create the Vault Environment

Vault creates resources in its own namespace: vault. 

Create a “vault” namespace as a Nirmata environment.

To create a new Environment, select Environment from the sidebar menu. Then click,  *+Add Environment* and complete the information in the pop-up window using the name “vault.” Click *Add*.

![image](/images/vault-3.png)

The new environment appears in the *Environments* list.

![image](/images/vault-4.png)

#### Create the Vault Application Space and Upload YAML Files

Now, create a new application in the Vault environment using the supplied YAMLs.

**Vault Application YAMLs:**
[etcd-operator-deploy.yaml](https://github.com/coreos/vault-operator/blob/master/example/etcd-operator-deploy.yaml)
[deployment.yaml](https://github.com/coreos/vault-operator/blob/master/example/deployment.yaml)
[example-vault.yaml](https://github.com/coreos/vault-operator/blob/master/example/example_vault.yaml)

To create a new application, add each YAML to the Application Catalog. Select *Catalog* in the sidebar menu and then select *Application Catalog*. From the main *Application Catalog* screen, click *Add Application*. 

Drop the YAML file into the upload  box or select the file from the directory. 

![image](/images/vault-5.png)

**_DO NOT DEPLOY THE APPLICATION_**

Open the [RBAC template](https://github.com/coreos/vault-operator/blob/master/example/rbac-template.yaml) file and edit the service account and namespace lines as shown.

![image](/images/vault-6.png)

After editing the RBAC template, deploy the file via Kubectl to the new namespace by opening the cluster and the Cluster Settings menu. Then select *Launch Terminal* to run a Kubectl command.

![image](/images/vault-7.png)

Using a text editor, paste the new RBAC into rbac.yaml. On the cluster, the rbac.yaml will display as shown.

![image](/images/vault-8.png)

To deploy the rbac.yaml, run the Deploy RBAC Command in the same terminal window. Replace ‘default’ with the active namespace before running.

**Deploy RBAC Command:**

```
Command: sh
/ # kubectl -n default create -f rbac.yaml
```

#### Deploy Flannel Overlay

To deploy the Flannel Overlay, apply the Flannel Overlay YAML and using a Kubectl command.

**Apply Flannel Overlay Command:**

```
kubectl apply -f
```

[Flannel Overlay YAML](https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml)

#### How to Deploy the Vault Operator

To deploy the Vault Operator, deploy both the etcd operator and the deployment YAML.

To deploy the [etcd operator](https://github.com/coreos/vault-operator/blob/master/example/etcd-operator-deploy.yaml) , click on *Catalog* in the sidebar menu and then select *Application Catalog*. From the main Application Catalog screen, click *Add Application*. 

Wait at least ten minutes before deploying the [deployment YAML](https://github.com/coreos/vault-operator/blob/master/example/deployment.yaml) using the Kubectl Deploy Command, replacing ‘default’ with the active namespace.

**Kubectl Deploy Command:**

```
$ kubectl -n default get deploy
```

After deploying both the etcd operator and the deployment YAML, verify that an etcd and vault operator are running on the cluster.

{{%excerpt%}}