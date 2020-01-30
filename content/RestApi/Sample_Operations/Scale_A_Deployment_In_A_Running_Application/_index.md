+++
title = "Scale a Deployment in a running Application"
description = ""
weight=100
+++
{{%excerpt%}}
Request:

    PUT /environments/api/deploymentSpecs/1d6ef0d7-91df-452c-b8af-ebf91f3e6b09
    Accept: application/json
    Authorization: NIRMATA-API <key>

Request Body:

    {
      "replicas" : 3
    }

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    {
        "id" : "1d6ef0d7-91df-452c-b8af-ebf91f3e6b09",
        "service" : "Environments",
        "modelIndex" : "DeploymentSpec",
        "uri" : "/environments/api/deploymentSpecs/1d6ef0d7-91df-452c-b8af-ebf91f3e6b09",
        "parent" : {
            "id" : "00979b37-05be-4b09-b5c7-7af68cb7d0c6",
            "service" : "Environments",
            "modelIndex" : "Deployment",
            "uri" : "/environments/api/deployments/00979b37-05be-4b09-b5c7-7af68cb7d0c6",
            "childRelation" : "spec"
        },
        "createdBy" : "ritesh@nirmata.com",
        "createdOn" : 1526011140575,
        "modifiedBy" : "jim@nirmata.com",
        "modifiedOn" : 1526854556236,
        "generation" : 1,
        "ancestors" : [ {
            "modelIndex" : "Deployment",
            "uuid" : "00979b37-05be-4b09-b5c7-7af68cb7d0c6",
            "service" : "Environments"
        }, {
            "modelIndex" : "Application",
            "uuid" : "97a1352d-4a0c-44b7-8ca6-0e264a203a59",
            "service" : "Environments"
        }, {
            "modelIndex" : "Environment",
            "uuid" : "ca8b2b15-1920-4910-9c34-846bee4ce6fe",
            "service" : "Environments"
        }, {
            "modelIndex" : "Root",
            "uuid" : "0b02a1ac-fae0-4b49-86e9-ff7a421cdf5c",
            "service" : "Environments"
        } ],
        "additionalProperties" : { },
        "alarms" : [ ],
        "additionalProperties" : { },
        "minReadySeconds" : null,
        "paused" : null,
        "progressDeadlineSeconds" : null,
        "replicas" : 3,
        "revisionHistoryLimit" : 5,
        "selector" : {
            "matchLabels" : {
            "nirmata.io/application.run" : "shopme",
            "nirmata.io/environment.name" : "centos-env",
            "nirmata.io/service.name" : "deals",
            "nirmata.io/application.name" : "shopme",
            "nirmata.io/component" : "deals"
            },
            "matchExpressions" : [ ]
        },
        "strategy" : [ {
            "id" : "cdc7cb74-6f27-4908-a358-55e4d79205e8",
            "service" : "Environments",
            "modelIndex" : "DeploymentStrategy",
            "uri" : "/environments/api/deploymentStrategies/cdc7cb74-6f27-4908-a358-55e4d79205e8"
        } ],
        "template" : [ {
            "id" : "b53af823-dbdd-41d9-b08f-e1c37378b7e9",
            "service" : "Environments",
            "modelIndex" : "PodTemplateSpec",
            "uri" : "/environments/api/podTemplateSpecs/b53af823-dbdd-41d9-b08f-e1c37378b7e9"
        } ]
    }

{{%/excerpt%}}
