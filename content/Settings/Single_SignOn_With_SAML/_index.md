+++
title = "Single Sign-On with SAML"
description = ""
weight=20
+++
{{%excerpt%}}
For Enterprise accounts, Nirmata supports Single Sign-On (SSO) with SAML
2.0. This feature allows enterprise administrators to manage their users
in a secure and easy manner. For example, when an employee is on-boarded
to, or leaves, the enterprise the administrators can enable, or disable,
their account in a single place for all enterprise services. This
feature also makes life easier for enterprise users as they can
authenticate once, and access all enabled services without managing
separate passwords and accounts.

SAML (Security Assertions Markup Language) is a protocol that defines
how systems can exchange security data. The following references are
useful in understanding SAML:

-   [SAML 2.0 - Wikipedia](https://en.wikipedia.org/wiki/SAML_2.0)
-   [SAML Introduction - XML.org](http://saml.xml.org/wiki/saml-introduction)

The SAML protocol is defined at: [Security Assertion Markup Language
(SAML) V2.0 Technical Overview -
OASIS](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html).

Although SAML is a complex protocol, Nirmata makes it extremely easy to
setup and manage. Here are the detailed steps:

1)  In your Account view ([Settings -\>
    Account](https://www.nirmata.io/webclient/#account)) select the
    option \"Enable Single Sign-On with SAML\":

![image](/images/SAML-1.png)

2) This option provides a dialog where you can upload the SAML metadata
file of your Identity Provider (IdP) e.g. ADFS 3.0. Or, you can manually
configure your IdP settings.

SAML IdP Metadata import:

![image](/images/SAML-2.png)

SAML IdP manual configuration:

![image](/images/SAML-3.png)

3) Next, export your account's Nirmata SAML Service Provider (SP)
metadata and import that into your IdP. To export the SP Metadata go to
[Settings - SAML
2.0](https://www.nirmata.io/webclient/#identityProvider) and click on
the View SP Metadata option. You can then copy the metadata or download
it to a file.

![image](/images/SAML-4.png)

To complete the setup, you can now import the SAML SP Metadata into your
IdP. If you are using Microsoft AD FS (Active Directory Federation
Services) follow the steps at [Setup AD FS for use with Nirmata](/settings/#setup-adfs) to configure ADFS for SSO with Nirmata.

Thats it! You now have SAML fully configured!

**Note:** By default, self-signed certificates are used to sign and encrypt
the data. In order to use CA signed certificates, see
[Using CA signed SAML signature certificates](/settings/#using-ca-certs).
{{%/excerpt%}}
