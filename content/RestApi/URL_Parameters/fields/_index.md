+++
title = "fields"
description = ""
weight=30
+++
{{%excerpt%}}
The fields parameter is used to control which fields, of an resource,
should be included in the JSON response. The fields parameter can be
applied to any GET request. The fields parameter value is specified as a
single field name, or a comma separated list of field names, that should
be included in the response.

For example, this query returns only the *id* and *name* fields of all
Deployments in the catalog:

    GET  http://www.nirmata.io/catalog/api/deployments?fields=id,name,kind,apiVersion
    Accept: application/json
{{%/excerpt%}}
