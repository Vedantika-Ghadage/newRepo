+++
title = "excludeFields"
description = ""
weight=40
+++
{{%excerpt%}}
The excludeFields parameter is used to exclude one or more fields from
the response. The excludeFields parameter can be applied to any GET
request. The fields parameter value is specified as a single field name,
or a comma separated list of field names, that should be excluded from
the response.

For example, this query excludes the *metadata* field from Deployments:

    GET  http://www.nirmata.io/catalog/api/deployments?excludefields=metadata
    Accept: application/json
{{%/excerpt%}}
