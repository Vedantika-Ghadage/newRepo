+++
title = "Microsoft Azure Cloud Provider"
description = ""
weight=30
+++
{{%excerpt%}}

Nirmata utilizes Azure Active Directory for
authentication. Be sure that Azure Active
Directory is setup before adding Microsoft Azure as a Cloud Provider in Nirmata. 

[Click here for instructions on setting up Azure Active Directory.](https://azure.microsoft.com/en-us/documentation/services/active-directory/)

To add Microsoft Azure as a Cloud Provider in Nirmata, enter the Subscription ID, Tenant ID,
Client ID, and Client Secret. 

#### How to Obtain Client ID

To find a Client ID in Microsoft Azure, login to the Azure account and use the sidebar menu to navigate to the active directory created for Nirmata. Open Settings and note the *Application ID.* 

**Note:** Application ID and Client ID are the same.

![image](/images/azurecloudprovider-1.png)

#### Create an Azure Application for Nirmata

Next, [create an Azure Application in the Resources Group of Azure](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad). This application will be used for Nirmata deployment.

To create an Azure Application, sign in to the Azure portal. 

From the sidebar menu, select *Azure Active Directory* and then *App Registration*.

Select *New Application Registration*.

![image](/images/azurecloudprovider-2.png)

In the *Create* page, enter the application registration information. 

Enter <https://www.nirmata.io> as the Webpage/API interface. Use the same Subscription ID as the current Resource Group.

![image](/images/azure-subscription-id.png)

Locate the Directory ID (Tenant ID) by opening the Azure Active Directory and then navigating to Properties. Note the Directory ID (Tenant ID).

![image](/images/azurecloudprovider-3.png)

#### Generate the Client Secret (Client Key)

The Client Secret (Client Key) is required to for Nirmata access to the Azure Application.

To create a Client Secret (Client Key) in Microsoft Azure, open the Azure Application and then Settings.

![image](/images/azurecloudprovider-4.png)

Select *Keys* and make note copy the key value.

![image](/images/azurecloudprovider-5.png)
 
#### Cohesive Environment Requirements

Confirm that all nodes can communicate and will allow Nirmata to create a Host Group. 

**Verify Active Resource Group for the Cluster**

Fist, confirm there is an active Resource Group for the cluster.

Sign in to the Azure portal. Sign in to the Azure portal and select *Resource Groups* from the sidebar menu. 

Select *+Add* and provide a name and location for the resource group. Click *Create.*

![image](/images/azurecloudprovider-6.png)

Click *Refresh* to view the newly created Resource Group.

![image](/images/azurecloudprovider-7.png)

**Confirm Security Groups are Configured Correctly**

[Review Microsoft Azure security groups](https://docs.microsoft.com/en-us/azure/virtual-network/security-overview) and apply the correct security levels.

**Confirm Accessible Storage Account**

Click here for instructions on creating an [Accessible Storage Account](https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-account?tabs=portal).

**Note:** If the cluster requires public access, be sure to allow public IP's to
 the nodes and to configure the networking security groups to allow *ssh*.

For a increased security, create a bastion host in the same subnet with a public IP. Then ssh to each node from a single point.

#### Add Cloud Provider to Nirmata

Select *Cloud Providers* from the sidebar menu. 

Complete the information in the *Add Cloud Provider* wizard.

Enter Cloud Provider information then click *Next.*

![image](/images/azurecloudprovider-9.png)

Enter Cloud Provider settings then click *Next.*

![image](/images/azurecloudprovider-10.png)

Nirmata automatically validates account access.
Once account access is validated, setup an [Azure Host Group](https://docs.nirmata.io/hostgroups/microsoft_azure_host_groups/).

**Next Steps**: Setup a [`azure-host-group`](/hostgroups/#azure-host-group)
Host Group.

{{%/excerpt%}}
