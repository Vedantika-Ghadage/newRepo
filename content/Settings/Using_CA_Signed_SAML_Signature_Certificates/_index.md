+++
title = "Using CA signed SAML Signature Certificates"
description = ""
weight=30
+++
{{%excerpt%}}
In order to use CA signed SAML signature certificates you can add the
certificates in the Service Provider Settings section.

![image](/images/settings-sp-data.png)

Next, export your account's Nirmata SAML Service Provider (SP) metadata
and import that into your IdP. To export the SP Metadata go to [Settings - SAML 2.0](https://www.nirmata.io/webclient/#identityProvider) and
click on the View SP Metadata option. You can then copy the metadata or
download it to a file.

To complete the setup, you can now import the SAML SP Metadata into your
IdP.
{{%/excerpt%}}
