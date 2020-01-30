+++
title = "AWS Cloud Provider - Cloud Edition"
description = ""
weight=20
+++

{{%excerpt%}}
Nirmata requires read-only access to EC2 service if using ASGs or Spot
Fleet Requests and full access to EC2 service if using Launch
Configuration to provision your VMs. The secure way to provide access is
by configuring an IAM role for Nirmata in your AWS account. To configure
a role, you will need the Nirmata AWS account ID and an unique external
ID. When the role is configured, you provide Nirmata the role ARN
(Amazon Resource Name).

This process may seem involved, but only takes a few minutes to set up!
Here are the detailed steps:

1.  Launch the Add Cloud Provider Wizard and select AWS as the provider.
![image](/images/AWS-IAM-Role-0.png)
2.  The Settings page with show you the Nirmata Account
    ID (094919933512) and a unique external ID for the Cloud Provider.
    You will require these in a later step:
    ![image](/images/AWS-IAM-Role-6.png)
3.  Login to your AWS account. Select IAM and navigate to the option to
    create a new user role:
![image](/images/AWS-IAM-Role-1.png)
![image](/images/AWS-IAM-Role-2.png)
![image](/images/AWS-IAM-Role-3.png)
4.  Select the 'Another AWS account' role type, and enter the Nirmata
    Account ID from the Settings page (Step 2):
![image](/images/AWS-IAM-Role-5-1.png)
5.  On the next page, select the 'AmazonEC2ReadOnlyAccess' and
    'IAMReadOnlyAccess' to allow Nirmata to provision EC2 instances:
![image](/images/AWS-IAM-Role-8-1.png)
You can also create a new custom policy (e.g. NirmataAutomationPolicy)
for more granular access control. Below is the Policy Document that can
be used in the custom policy. This policy limits
Start/Stop/TerminateInstance to the instances created by Nirmata with
appropriate tag:
``` json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ec2:RunInstances",
                    "ec2:CreateTags",
                    "ec2:Describe*"
                ],
                "Resource": [
                    "*"
                ]
            },
            {
                "Effect": "Allow",
                "Action": [
                    "ec2:StartInstances",
                    "ec2:StopInstances",
                    "ec2:TerminateInstances"
                ],
                "Resource": "arn:aws:ec2:<region>:<account>:instance/*",
                "Condition": {
                    "StringEquals": {
                        "ec2:ResourceTag/com.nirmata.createdBy": "nirmata"
                    }
                }
            },
            {
                "Effect": "Allow",
                "Action": "autoscaling:Describe*",
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": [
                    "iam:GetRole",
                    "iam:ListAttachedRolePolicies",
                    "iam:ListPolicyVersions",
                    "iam:ListInstanceProfiles",
                    "iam:GetPolicyVersion",
                    "iam:SimulateCustomPolicy",
                    "iam:PassRole"
                ],
                "Resource": "*"
            }
        ]
    }
```
{{% notice note %}} Be sure to replace the **\<region\>** and **\<account\>**
placeholders, with the allowed region or "\*" to allow all regions,
and your AWS account ID.{{% /notice %}}

6.  Provide a name (e.g. 'nirmata-aws-role-1') and click on Create
    role:
![image](/images/AWS-IAM-Role-4-1.png)
7.  Finish creating the AWS IAM role. Go to the roles page and select
    the role you just created and copy the Role ARN:
![image](/images/AWS-IAM-Role-11.png)
8.  Paste the Role ARN into the Nirmata Add Cloud Provider Wizard. You
    can then click 'Next' and Nirmata will validate the settings:
![image](/images/AWS-IAM-Role-12.png)

{{% notice note %}} When deploying a Kubernetes cluster on AWS Host Groups, an IAM
policy for the hosts in the cluster need to be created. This IAM policy
allows the AWS cloud controller to access AWS resources.{{% /notice %}}

An example of the IAM policies can be found here:

Master Nodes:
<https://github.com/kubernetes/kops/blob/master/pkg/model/iam/tests/iam_builder_master_strict.json>

Compute Nodes:
<https://github.com/kubernetes/kops/blob/master/pkg/model/iam/tests/iam_builder_node_strict.json>

For networking, Nirmata uses Amazon VPC CNI plugin
(<https://github.com/aws/amazon-vpc-cni-k8s>). This plugin requires the
following IAM policy:
``` JSON
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
```
##### Creating AWS Cloud Provider Video
<iframe width="854" height="510" src="https://www.youtube.com/embed/5LPVg5ksXvI" frameborder="0" allowfullscreen></iframe>

**Next Steps**: Setup a [`aws-host-group`](/hostgroups/#aws-host-group)
Host Group.
{{%/excerpt%}}
