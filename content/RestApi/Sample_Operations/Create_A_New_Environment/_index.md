+++
title = "Create a new Environment"
description = ""
weight=70
+++
{{%excerpt%}}
Request:

    POST /api/environments/
    Accept: application/json
    Authorization: NIRMATA-API <key>

    {
      "name": "dev-test",
      "hostCluster": {"name" : "devtest-aks-us-east"}
    }

Note the different ways you can specify a relation in the JSON. For a 1-1 relationship you can:

  1.  Specify an UUID
  2.  Specify a JSON object with fields that can be used to find the relation. In the example above, we use the name field to query the  Cluster.
{{%/excerpt%}}
