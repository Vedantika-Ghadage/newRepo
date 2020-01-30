+++
title = "Secrets"
description = ""
weight=60
+++
{{%excerpt%}}
Secrets can be created to store sensitive information such as password,
certificates etc. Putting sensitive information in secrets is relatively
secure compared to including it in your container image and provides
flexibility in how these secrets can be accessed.

Secrets can be made available to your pod as:

 1.  Environment variables
 2.  Volumes

A Secret can be shared across multiple pod templates further simplifying
your application configuration.
{{%/excerpt%}}
