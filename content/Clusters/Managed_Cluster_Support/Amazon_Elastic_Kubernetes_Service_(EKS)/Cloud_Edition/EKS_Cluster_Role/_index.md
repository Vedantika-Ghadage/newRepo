+++
title = "Amazon EKS Cluster Role"
description = ""
weight=20
+++

In addition to adding AWS as a Cloud Provider, managing an EKS Cluster in Nirmata requires another role for EKS service in AWS.

To create this role required for EKS Cluster management in Nirmata, login to the AWS Management Console and select IAM Services.

Select Roles and then click on the button to Create Role.

![image](/images/eks-4.png)

Select AWS Service and then select EKS under available services.

![image](/images/eks-5.png) ![image](/images/eks-6.png)

Look for EKS policies as shown below

]![image](/images/eks-7.png)

Apply the following policies to the role:

AmazonEKSClusterPolicy
AmazonEKSServicePolicy

Locate each permission by entering the Permission Name into the Search box. Place a checkmark next to each required permission. After adding all permissions, click the Create Policy button.

![image](/images/eks-8.png)

Complete the role creation process. 

![image](/images/eks-9.png)

In Nirmata, you will use this role in the EKS ARN role field as shown below.

![image](/images/eks-10.png)