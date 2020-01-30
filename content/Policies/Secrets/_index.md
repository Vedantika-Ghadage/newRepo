+++
title = "Secrets"
description = ""
weight=20
+++
{{%excerpt%}}
Secrets policies is used to provide environment specific secrets for
your applications. For example, if you have an application that uses a
database and you want to enable different secrets in different
environments, e.g. Development vs Production, you can use the Config Map
policy to provide the secrets instead of creating and managing different
application manifests. This makes your application manifests more
portable.

##### Creating a Secret Policy

To create a secret policy, you need to provide:

 -   Name: Name of the policy
 -   Application Selector: Selects the application to which this policy will be applied
 -   Data: Secret key/value pairs that should be added to your application.
{{%/excerpt%}}
