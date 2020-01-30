+++
title = "Private Cloud"
description = ""
weight=100
+++
{{%excerpt%}}

Nirmata can securely manage your VMware and OpenStack cloud resources,
and Docker Image Registries, in your Data Center. To connect your
Private Cloud, you will need to run the Nirmata Private Cloud Agent, on
a system within your Data Center that has connectivity to your cloud
management system (e.g. VMware's vCenter) and/or your private Docker
Image Registry. Once the Nirmata Private Cloud Agent is connected, you
can then provision Cloud Providers and Image Registries and select the
appropriate private cloud for these systems.

To setup a Private Cloud first, navigate to Settings and then select *Private Cloud*. Select the option to *Add Private Cloud*.
Enter a unique name for the new Private Cloud.

![image](/images/privatecloud-1.png)

Next, setup a system in your Data Center for the Nirmata Private Cloud agent. Run the Install Agent Command, using the unique ID for the new Private Cloud:

**Install Agent Command:**

```
curl -sSL https://www.nirmata.io/nirmata-private-cloud-agent/setup-nirmata-private-cloud-agent.sh | sudo sh -s b71025b0-068f-40a1-8804-f03e52c598db
```

After the Private Cloud is connected, select it when creating an
Image Registry, a VMware vSphere Cloud Provider, or an OpenStack Cloud
Provider.

![image](/images/privatecloud-1.png)

{{%/excerpt%}}
