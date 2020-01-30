+++
title = "Amazon EKS - Private Edition"
description = ""
weight=20
+++

#### EKS: Deploymnent Prerequisites

EKS Deployment requires a few things to be in-place before you deploy the cluster through Nirmata:

1. **VPC:** Create IP Address block for your EC2 instances.

2. **Network Group:** Any AWS setup requires you to setup a network group with subnet policy which will be used to provide connectivity across your EC2 instances.

3. **Security Group:** Security group defines that security policy for access into and between your EC2 instances. Security policy is core construct needed to setup your AWS services. For an EKS cluster, two security groups are recommended - control-plane security group for cluster operations and worker node security group for application traffic. For control plane security group, for inbound traffic, ports 443  from all nodes in worker security group are recommended. For outbound traffic, ports 1025-65535 are recommended to be open. Port 10250 is minimum requirement. For worker security group, port 443 and port-range 1025-65535 is recommended to be open. For outbound traffic, all ports can be open. [Click here for more information.](https://docs.aws.amazon.com/eks/latest/userguide/sec-group-reqs.html)

4. **Nirmata EC2/EKS User:**   An EC2 user that can provision EKS control-plane and EC2 instances through Nirmata is required for the cloud provider integration. You can create an [EC2 user](./create_user_for_eks_cluster/) with necessary permission for Nirmata or use an existing user with right permissions.

5. **Nirmata EKS Role:** AWS requires an additional role to create and manage the EKS cluster resources. [Click here](../cloud_edition/eks_cluster_role/) for a step-by-step introduction on creating an IAM role for EKS.

6. **AWS account ID and access key credentials:** To make API calls into AWS resources, create an access key with an ID and secret key for the EC2 user created. You will use both to configure the Cloud Provider integration required for EKS setup.

7. **Nirmata Cloud Provider:** In Nirmata UI, configure the Cloud Provider integration with options as shown below. Use the account ID and secret key previously configured.

![image](/images/EKS-Deployment0.png)

To access the *Edit Cloud Provider* options, select *Cloud Providers* from the sidebar menu. Then click on the *Edit* icon.


##### Create AWS User for Nirmata EC2/EKS configuration

Nirmata requires permissions to create EKS cluster control-plane and EKS compliant EC2 workder nodes. Those permissions are assigned to a user specifically created for this purpose. You can follow the instructions shared [here](./create_user_for_eks_cluster/).



#### EKS Configuration Steps

![image](/images/eks-1.png)

To create an EKS cluster, select *Clusters* from the sidebar menu and then click *+Add Cluster*. Choose *Create EKS cluster.*

![images](/images/EKS-Deployment1.png)


1. **Cloud Provider**- This is the cloud provider configuration your created for API integration using the EC2 role defined. Choose the right option from the drop down menu.
   
2. **Region** - Please pick the region where you would like to create the EKS cluster.
   
3. **Kubenetes version** - Please pick an option from one of the EKS supported versions for Kubernetes.
   
4. **VPC ID** - This is the virtual private cloud ID you created when setting up your EC2 instance.
   
5. **Networks** - Please pick from network groups you had created. You need to pick at least 2 groups.
   
6. **Security group** - Please pick from drop down menu the security group configured in Step-3.
   
7.  **Cluster Role ARN** - This is the EKS cluster role you created in Step-5 for Nirmata to deploy EKS. Again, with cloud provider integration, you should see it in the drop down menu.


Then complete the following parameters:

![image](/images/EKS-Deployment2.png)


1. **Instance Type:** Pick from EC2 instance type you would like to use for EK cluster.

2. **Image ID:** Pick EKs compliant image supported for the intance type.

3. **Autoscaling group desired capacity:** Configure desired number of nodes to begin the cluster setup.

4. **Autoscaling group min size:** Configure minimum node scale required for the cluster.

5. **Autoscaling group max size:** Configure maximum number of nodes required for the cluster.

6. **SSH Key**- Pick the SSH key ID from the drop-down menu.
   
7. **Disk size**- Pick the disk size of the EKS cluster nodes.

After complete the configuration steps, click *Create Cluster.* Your new cluster will be ready in 10 to 15 minutes. 

**NOTE: If you are creating a cluster in private address space and have not routed a connection back to the Nirmata controller, you will be able to create the cluster but not connect it back to Nirmata You will see a broken routing error.**