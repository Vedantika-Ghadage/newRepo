+++
title = "Amazon ECR"
description = ""
weight=30
+++
{{%excerpt%}}
To securely connect Nirmata with Amazon ECR first setup an AWS Cloud
Provider. When setting up the cloud provider, ensure that
AmazonEC2ContainerRegistryFullAccess is selected.

![image](/images/ecr-setup.png)

Next, add the Image Registry in Nimrata. Enter the name, select Amazon
ECR as the provider, enter the location and select cloud provider.
Ensure that this cloud provider is using an IAM role that has policy
AmazonEC2ContainerRegistryFullAccess enabled.

The registry location can found from the Amazon ECR page.

![image](/images/ecr-repo-view.png)

![image](/images/add-ecr.png)

Once the repository is added, you can view the images in that registry
as well as the tags for each image repository. Now you can select the
tag when creating a new service for an image.
{{%/excerpt%}}
