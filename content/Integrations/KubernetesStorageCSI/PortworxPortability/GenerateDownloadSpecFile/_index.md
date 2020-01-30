+++
title = "Generate and Download a Portworx Spec File"
description = ""
weight=60
+++
{{%excerpt%}}

To create a Portworx Spec File, use the Portworx Spec Generator for the appropriate Portworx version.

[Click here to access all available Portworx Spec Generators.](https://docs.portworx.com/scheduler/kubernetes/install.html#install)

The Portworx Spec Generator steps through the process and requests information at each step. 

Start by entering the Kubernetes version, selecting an etcd, and a region. 

![image](/images/portworx-2.png)

Then select a Cloud Provider and cloud-provider specific details.

![image](/images/portworx-3.png)

Next, complete the network data based on the appropriate interface devices. 

![image](/images/portworx-4.png)

Finally, select customization options and click *Finish*.

![image](/images/portworx-5.png)

![image](/images/portworx-6.png)

The Portworx Spec Generator creates a spec URL. Download the spec file. The spec file downloads a YAML.

![image](/images/portworx-7.png)

{{%/excerpt%}}