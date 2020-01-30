+++
title = "URL Parameters"
description = ""
weight=40
+++
{{%excerpt%}}
URL Parameters are used to control the returned JSON data.

##### mode

The mode parameter is used to control the JSON output format for a GET request. Here are the allowed values:

  -   normal
  -   export
  -   exportDetails

In the *normal* mode the JSON data for each object contains
all attributes and relations are output as links. In the
*export* mode the JSON data contains all attributes and
child relation objects are directly embedded into the parent. Reference
relations are represented as links, and also contain the unique
attributes of the referred to object. The mode parameter can be applied
to all GET requests and can be combined with other parameters. The
export mode is useful when an entire sub-document needs to be retrieved
and stored externally. For example, the following query will export the
full {model} as JSON:

    GET http://www.nirmata.io/catalog/api/applications/{id}?mode=export
    Accept: application/json

The *exportDetails* mode also includes meta-data fields and
relations to external entities (outside of the target document).

##### query

The query parameter is used to control which objects are included in a
JSON response. The query data is specified as a JSON object. The query
parameter can be applied to any GET request that returns multiple
objects. For example the following query returns the application named
'helloworld':

    GET  http://www.nirmata.io/environments/api/applications?query={"name":"helloworld"}
    Accept: application/json

Multiple attributes can be specified for a logical AND operation:

    GET  http://www.nirmata.io/environments/api/applications?query={"name":"helloworld", "run" : "hello1"}
    Accept: application/json

##### fields

The fields parameter is used to control which fields, of an resource,
should be included in the JSON response. The fields parameter can be
applied to any GET request. The fields parameter value is specified as a
single field name, or a comma separated list of field names, that should
be included in the response.

For example, this query returns only the *id* and *name* fields of all
Deployments in the catalog:

    GET  http://www.nirmata.io/catalog/api/deployments?fields=id,name,kind,apiVersion
    Accept: application/json

##### excludeFields

The excludeFields parameter is used to exclude one or more fields from
the response. The excludeFields parameter can be applied to any GET
request. The fields parameter value is specified as a single field name,
or a comma separated list of field names, that should be excluded from
the response.

For example, this query excludes the *metadata* field from Deployments:

    GET  http://www.nirmata.io/catalog/api/deployments?excludefields=metadata
    Accept: application/json

##### count

The count parameter is used to specify the maximum number of resources
to be returned. It can be used when querying a relation, a list of
resources, or using a query parameter. A positive value is expected.
When not specified, all matching resources are returned. For example the
following query returns the podIP and state fields for up to 10
instances of the resource *podStatus*:

    GET  http://www.nirmata.io/environments/api/podStatus?count=10&fields=podIP,state
    Accept: application/json

##### start

The start parameter is used to specify the start index in a list of
resources. It can be used when querying a relation, a list of resources,
or using a query parameter. A positive value is expected. When not
specified a value of 0 is assumed. For example the following query
returns *podStatus* instances 10-20 (or less) that have attribute state
with the *state* of *running*:

    GET  http://www.nirmata.io/environments/api/podStatus?start=10&count=10&query={"state" : "running"}&fields=id
    Accept: application/json

{{%/excerpt%}}
