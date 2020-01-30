+++
title = "Config Maps"
description = ""
weight=10
+++
{{%excerpt%}}

Config Map policies are used to provide environment specific
configuration for your applications. For example, if you have an
application that uses a proxy such as nginx and you want to enforce
specific configuration in different environments, e.g. Development vs
Production, you can use the Config Map policy to provide the
configuration instead of creating and managing different application
manifests. This makes your application manifests more portable.

{{%excerpt-include filename="Policies/Config_Maps/Creating_A_Config_Map_Policy/_index.md" /%}}

{{%/excerpt%}}
