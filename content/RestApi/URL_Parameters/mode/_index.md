+++
title = "mode"
description = ""
weight=10
+++
{{%excerpt%}}
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
{{%/excerpt%}}
