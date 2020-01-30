+++
title = "Patch Policy"
description = ""
weight=30
+++
{{%excerpt%}}
A patch policy allows you to override settings in your Kubernetes
Resource manifests for a selected namespace. For example, if you want to
use specific load balancer settings for certain applications you can
configure a patch policy for the Service Resource to add annotations for
Load Balancer settings.

To create a patch policy, you need to provide:

 -   Name: Name of the policy
 -   Resource Type: Kubernetes resource type
 -   Namespace Selector: Selects the namespace to which this policy will be applied
 -   Patch Operations: The operation that should be performed on the selected resource

To add a patch operation, you need to provide:

 -   Path: The path for the property in the Kubernetes resource (e.g. /metadata/annotations/service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout)
 -   Operation: The operation that needs to be performed. Possible operations are: add, replace, remove
 -   Value Type: The type of the value. Possible types are: text, number, json string
 -   Value: The actual value to apply

#### How to Create a New Patch Policy

Click on *Policies* in the sidebar menu and select *Patch Policies*. Click on the *+ Add Patch Policy* button.

![image](/images/patch-policy-1.png)

Name the Patch Policy and then choose a *Resource Type*, and *Service Selector* and click *Add*.

![image](/images/patch-policy-2.png)

The new policy is displayed.

![image](/images/patch-policy-3.png)


{{%/excerpt%}}
