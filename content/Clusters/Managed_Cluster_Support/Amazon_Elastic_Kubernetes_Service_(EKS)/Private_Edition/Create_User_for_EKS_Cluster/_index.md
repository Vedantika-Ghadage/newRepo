+++
title = "Create a User for Amazon EKS"
description = ""
weight=20
+++

For Nirmata Private Edition, you will need to create an AWS User with necessary permissions to provision EC2 worker nodes as well as create EKS control plane. For the user, you will use the user access id and secret key to configure AWS Cloud Provider in Nirmata.

First, you need create a policy with specific permissions for the User. login to the AWS Management Console and select IAM Services. Click on Policies under AWS IAM screen and choose "Create Policy" button.

![image](/images/Select-Policy-EKS-User.png)

Under Policy, choose JSON, and copy and paste the permissions as highlighted below - 

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ec2:TerminateInstances",
                "ec2:StartInstances",
                "ec2:StopInstances"
            ],
            "Resource": "arn:aws:ec2:*:094919933512:instance/*",
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/com.nirmata.createdBy": "nirmata"
                }
            }
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "iam:GetPolicyVersion",
                "autoscaling:Describe*",
                "iam:ListInstanceProfilesForRole",
                "iam:PassRole",
                "iam:SimulateCustomPolicy",
                "iam:ListAttachedRolePolicies",
                "iam:ListAttachedUserPolicies",
                "iam:ListAttachedGroupPolicies",
                "iam:ListRolePolicies",
                "iam:ListPolicies",
                "iam:GetRole",
                "iam:GetPolicy",
                "iam:ListGroupPolicies",
                "ec2:CreateTags",
                "iam:ListRoles",
                "ec2:RunInstances",
                "iam:ListUserPolicies",
                "iam:ListInstanceProfiles",
                "ec2:Describe*",
                "iam:ListPolicyVersions",
                "iam:GetUserPolicy",
                "iam:ListGroupsForUser",
                "iam:ListUsers",
                "iam:GetGroupPolicy",
                "iam:GetUser",
                "iam:GetRolePolicy",
                "iam:GenerateCredentialReport",
                "iam:GenerateServiceLastAccessedDetails",
                "iam:Get*",
                "iam:List*",
                "iam:SimulateCustomPolicy",
                "iam:SimulatePrincipalPolicy",
                "iam:GetPolicyVersion",
                "iam:SimulateCustomPolicy",
                "iam:GenerateCredentialReport",
                "iam:GenerateServiceLastAccessedDetails",
                "iam:Get*",
                "iam:List*",
                "iam:SimulateCustomPolicy",
                "iam:SimulatePrincipalPolicy",
                "iam:CreateRole",
                "iam:DeleteRole",
                "iam:AttachRolePolicy",
                "iam:DetachRolePolicy",
                "iam:CreateInstanceProfile",
                "iam:DeleteInstanceProfile",
                "iam:AddRoleToInstanceProfile",
                "iam:RemoveRoleFromInstanceProfile"
            ],
            "Resource": "*"
        },
        {
            "Sid": "VisualEditor2",
            "Effect": "Allow",
            "Action": [
                "cloudformation:CreateStack",
                "cloudformation:DeleteStack",
                "cloudformation:CreateChangeSet",
                "cloudformation:UpdateStack",
                "cloudformation:ExecuteChangeSet",
                "cloudformation:Describe*",
                "cloudformation:EstimateTemplateCost",
                "cloudformation:Get*",
                "cloudformation:List*",
                "cloudformation:ValidateTemplate",
                "cloudformation:DetectStackDrift",
                "cloudformation:DetectStackResourceDrift"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "VisualEditor3",
            "Effect": "Allow",
            "Action": "eks:*",
            "Resource": "*"
        }
    ]
}
```
Click "Review Policy" and then save the policy. 

Now, you can create a User required for EC2 and EKS Cluster management in Nirmata that will use this Policy. For that, login to the AWS Management Console and select IAM Services.

Select Users and then click on the button to Add a User.

![image](/images/Add-User-EKS-PE.png)

Select programmatic access and then select "Next:Permission" button.

![image](/images/User-EKS-prog-acccess.png)

Choose "Attach existing policies directly" and select the policy you created above.

![image](/images/eks_add_user_select_policy.png)

Also add couple of AWS Managed Policies as well - 

AmazonEC2FullAccess
AmazonEC2ContainerRegistryReadOnly

![image](/images/permissions.png)

Now click on "Security Credentials" tab on the User menu and click on "Create Access Key". You can download the Access Key Id and secret key. You can add the Access Key ID and Nirmata

In Nirmata, you will use this role in the EKS ARN role field as shown below.

![image](/images/AWS-Cloud-Provider-EKS.png)