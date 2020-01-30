+++
title = "Deploy the Portworx Spec File in Nirmata"
description = ""
weight=70
+++
{{%excerpt%}}

Deploy the Portworx Spec File within Nirmata. 

Note that each configuration is different and that the devices used and network and management interfaces will vary based on the configuration.

To deploy the  Portworx Spec File via Nirmata, open the Nirmata terminal and enter the  Create YAML File command.

**Create YAML File Command:**
```
vi spec.yaml.
```

Save the contents of the  Portworx Spec File into the new file and deploy the YAML using a Deploy Kubectl Command.

**Deploy Kubectl Command:**
```
kubectl apply -f spec.yaml 
```

Allow a few minutes for the Portworx Spec File to setup. Then, SSH into any one of the worker nodes and run a Status Command.

**Status Command:**
```
 sudo /opt/pwx/bin/pxctl status
```

When properly configured in a two-disk setup, the following results will display: 

![image](/images/portworx-8.png)
{{%/excerpt%}}