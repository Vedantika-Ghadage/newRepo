+++
title = "Cloud Provider Integrations"
description = ""
weight=50
+++
{{%excerpt%}}
##### AWS

You can use AWS as a Kubernetes cloud provider to enable EBS, ELB, and
EC2 integrations. To do this, you need to configure an IAM role for
Kubernetes.

Below are the permissions that need to be enabled for this role. As a
best practice, you can customize the role to be limited to a sub-set of
resources:
```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "ec2:Describe*",
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": "ec2:AttachVolume",
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": "ec2:DetachVolume",
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": [
                    "ec2:*"
                ],
                "Resource": [
                    "*"
                ]
            },
            {
                "Effect": "Allow",
                "Action": [
                    "elasticloadbalancing:*"
                ],
                "Resource": [
                    "*"
                ]
            },
            {
                "Effect": "Allow",
                "Action": [
                    "ec2:CreateNetworkInterface",
                    "ec2:AttachNetworkInterface",
                    "ec2:DeleteNetworkInterface",
                    "ec2:DetachNetworkInterface",
                    "ec2:DescribeNetworkInterfaces",
                    "ec2:DescribeInstances",
                    "ec2:ModifyNetworkInterfaceAttribute",
                    "ec2:AssignPrivateIpAddresses"
                ],
                "Resource": [
                    "*"
                ]
            },
            {
                "Effect": "Allow",
                "Action": "tag:TagResources",
                "Resource": "*"
            }
        ]
    }
```
To create an AWS Host Group see the [Host Groups](/hostgroups/) section.

##### vSphere

Prior to deploying Kubernetes clusters on vSphere, see the [prerequisites](https://vmware.github.io/vsphere-storage-for-kubernetes/documentation/prerequisites.html)


**Note:** To enable vSphere storage to work, you need to enable
disk.EnableUUID option when creating the VM template. For instructions,
see the [FAQs](https://vmware.github.io/vsphere-storage-for-kubernetes/documentation/faqs.html).
{{%/excerpt%}}
