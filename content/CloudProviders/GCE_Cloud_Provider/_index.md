+++
title = "GCE Cloud Provider"
description = ""
weight=40
+++
{{%excerpt%}}

To add Google Compute Engine (GCE) as a Cloud Provider in Nirmata, add the Service Account Key.

#### Locate the Service Account Key in GCE

A GCE service account key allows services outside of Google Cloud Platform (GCP) to communicate with GCE.

To locate the service account key, login to GCP Console and open *IAM & admin.*

Select a project from the drop down menu and click *Open.*

![image](/images/gcecloud-1.png)

Select *Service Accounts* from the sidebar menu.

![image](/images/gcecloud-2.png)

Locate the service account, click the *More* more_vert button in that row, and then click *Create*.

Select the *Key Type* and click *Create.*

The `privateKeyData` returned is a base64-encoded string representation of the JSON or P12 key/credentials.

Save the JSON file in a secure, accessible location.

#### Add GCE Service Account Key to Nirmata

To add the GCE Service Account Key to Nirmata, select Cloud Providers from the sidebar menu. Select *+Add Cloud Provider*.

![image](/images/gcecloud-3.png)

Enter the *Cloud Provider* information. Select *Google Cloud Platform* as the *Type.* Click *Next.*

![image](/images/gcecloud-4.png)

On the *Settings* tab, drop the service account key JSON file or select from the file directory. Click *Next.*

![image](/images/gcecloud-5.png)

Nirmata automatically validates account access.
Once account access is validated, setup a [Google Host Group](https://docs.nirmata.io/hostgroups/gce_host_groups/).

**Next Steps**: Setup a [`gce-host-group`](/hostgroups/#gce-host-group)
Host Group.
{{%/excerpt%}}
