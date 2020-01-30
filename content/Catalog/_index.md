+++
title = "Catalog"
description = "Catalog information"
weight=70
+++

The Catalog stores Application definitions. You can easily model new
applications in the Catalog, and export them as Kubernetes YAML files.

![image](/images/concepts-catalog.png)

You can also import existing YAML files to compose an application or
create an application from a Helm Chart. You can then use access
controls for an application to make certain applications available to
select users, roles or teams.

![image](/images/catalog-applications.png)

An application can be composed of several stateless or stateful
components. For details on defining applications, see
[`applications`](/applications/#applications).

#### Import YAML files
{{%excerpt-include filename="Catalog/Import_YAML_Files/_index.md" /%}}

#### Import a Helm Chart
{{%excerpt-include filename="Catalog/Import_A_Helm_Chart/_index.md" /%}}

#### Import or Export an Application
{{%excerpt-include filename="Catalog/Import_Or_Export_An_Application/_index.md" /%}}

#### Access Controls
{{%excerpt-include filename="Catalog/Access_Controls/_index.md" /%}}
