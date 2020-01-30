+++
title = "Cloud Providers"
description = ""
weight=30
+++


A **Cloud Provider** is used to provide Nirmata access to your public or
private cloud resources.

The setup for any Cloud Provider has the following general flow:

  1.  Create the Cloud Provider in Nirmata
  2.  Prepare a VM template, or similar construct to provision cloud
        instances, as detailed in the [`host-groups`](#hostgroups) section.
  3.  Create one or more Host Groups in Nirmata

The setup for private clouds, has one additional step. You will first
need run the Nirmata Private Cloud Agent and then configure a Cloud
Provider. See details in the [`private-cloud-setup`](/cloudproviders/#private-cloud-setup) setup section.

#### Direct Connect {#direct-connect-provider}
{{%excerpt-include filename="CloudProviders/Direct_Connect/_index.md" /%}}

#### AWS Cloud Provider {#aws-provider}
{{%excerpt-include filename="CloudProviders/AWS_Cloud_Provider/_index.md" /%}}

#### Microsoft Azure Cloud Provider {#azure-provider}
{{%excerpt-include filename="CloudProviders/Microsoft_Azure_Cloud_Provider/_index.md" /%}}

#### GCE Cloud Provider {#gce-provider}
{{%excerpt-include filename="CloudProviders/GCE_Cloud_Provider/_index.md" /%}}


#### Oracle Cloud Provider {#opc-provider}
{{%excerpt-include filename="CloudProviders/Oracle_Cloud_Provider/_index.md" /%}}


#### Digital Ocean Cloud Provider {#digital-ocean-provider}
{{%excerpt-include filename="CloudProviders/VMware_vSphere_Cloud_Provider/_index.md" /%}}

#### VMware vSphere Cloud Provider {#vsphere-provider}
{{%excerpt-include filename="CloudProviders/VMware_vSphere_Cloud_Provider/_index.md" /%}}

#### OpenStack Cloud Provider {#openstack-provider}
{{%excerpt-include filename="CloudProviders/OpenStack_Cloud_Provider/_index.md" /%}}

#### Bare Metal Servers
{{%excerpt-include filename="CloudProviders/Bare_Metal_Servers/_index.md" /%}}

#### Private Cloud {#private-cloud-setup}
{{%excerpt-include filename="CloudProviders/Private_Cloud/_index.md" /%}}
