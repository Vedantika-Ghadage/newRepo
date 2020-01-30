+++
title = "Discover attributes and relations"
description = ""
weight=190
+++
{{%excerpt%}}
You can query a single class, to get its attributes and relations.

Request:

    curl -X OPTIONS -H "Accept: application/json" -H "Authorization: NIRMATA-API <key>" https://nirmata.io/config/api/ContainerType

Response Body:

    {
      "name" : "Config",
      "id" : "d05f7751-8dae-4733-9e14-601d6f3516b3",
      "rootIndex" : "Root",
      "modelClasses" : [ {
        "modelIndex" : "ContainerType",
        "uri" : "/config/api/containerTypes",
        "methods" : [ "OPTIONS", "GET", "POST", "DELETE", "PUT" ],
        "apiLabel" : "containerTypes",
        "isDeleteable" : true,
        "keyField" : "name",
        "parents" : [ "Root" ],
        "attributes" : [ {
          "name" : "name",
          "type" : "String",
          "isRequired" : true,
          "uniqueScope" : "PARENT",
          "isKey" : false,
          "length" : 0
        }, {
          "name" : "description",
          "type" : "String",
          "isRequired" : false,
          "uniqueScope" : "NONE",
          "isKey" : false,
          "length" : 0
        }, {
          "name" : "cpuShares",
          "type" : "Integer",
          "isRequired" : false,
          "uniqueScope" : "NONE",
          "isKey" : false,
          "min" : 0,
          "max" : 1024,
          "default" : 0
        }, {
          "name" : "memory",
          "type" : "Integer",
          "isRequired" : false,
          "uniqueScope" : "NONE",
          "isKey" : false,
          "min" : 0,
          "max" : 64000,
          "default" : 0
        } ],
        "relations" : [ {
          "name" : "resourceSelectionRules",
          "type" : "Reference",
          "relationClass" : "ResourceSelectionRule",
          "cardinality" : {
            "min" : 0,
            "type" : "zeroOrMore"
          },
          "isMany" : true,
          "relationField" : "containerTypes",
          "isStrongReference" : false,
          "uri" : "/config/api/containerTypes/{id}/resourceSelectionRules",
          "methods" : [ "OPTIONS", "GET" ]
        }, {
          "name" : "services",
          "type" : "Reference",
          "relationClass" : "Service",
          "cardinality" : {
            "min" : 0,
            "type" : "zeroOrMore"
          },
          "isMany" : true,
          "relationField" : "containerType",
          "isStrongReference" : false,
          "uri" : "/config/api/containerTypes/{id}/services",
          "methods" : [ "OPTIONS", "GET" ]
        } ]
      } ]
    }
{{%/excerpt%}}
