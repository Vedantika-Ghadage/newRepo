+++
title = "Update image version for a running container"
description = ""
weight=120
+++
{{%excerpt%}}
Request Headers:

    PUT /environments/api/containers/9bb53549-572c-499b-9bad-1d51079e13f2

Request Body:

    {
        "image" : "gcr.io/google-samples/gb-frontend:v6"
    }

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    {
        "id" : "9bb53549-572c-499b-9bad-1d51079e13f2",
        "service" : "Environments",
        "modelIndex" : "Container",
        "uri" : "/environments/api/containers/9bb53549-572c-499b-9bad-1d51079e13f2",
        "tenantId" : "45b34043-2844-48ca-b14c-a1944d322c8c",
        "parent" : {
            "id" : "6f40ca06-80c7-4a56-b582-5e05586b3b49",
            "service" : "Environments",
            "modelIndex" : "PodSpec",
            "uri" : "/environments/api/podSpecs/6f40ca06-80c7-4a56-b582-5e05586b3b49",
            "childRelation" : "containers"
        },
        "createdBy" : "Nirmata",
        "createdOn" : 1526333823626,
        "modifiedBy" : "jim@nirmata.com",
        "modifiedOn" : 1526855075468,
        "generation" : 1,
        "ancestors" : [ {
            "modelIndex" : "PodSpec",
            "uuid" : "6f40ca06-80c7-4a56-b582-5e05586b3b49",
            "service" : "Environments"
        }, {
            "modelIndex" : "Pod",
            "uuid" : "e0d8c535-fd4f-4a5c-a36c-2defbbc1f124",
            "service" : "Environments"
        }, {
            "modelIndex" : "Application",
            "uuid" : "343b46f2-6b93-45ac-b38b-bdbc2d133f1e",
            "service" : "Environments"
        }, {
            "modelIndex" : "Environment",
            "uuid" : "37594c41-bbb3-4ee4-a04c-a84cc2ca7a10",
            "service" : "Environments"
        }, {
            "modelIndex" : "Root",
            "uuid" : "0b02a1ac-fae0-4b49-86e9-ff7a421cdf5c",
            "service" : "Environments"
        } ],
        "additionalProperties" : {
            "envFrom" : [ ]
        },
        "alarms" : [ ],
        "name" : "php-redis",
        "image" : "gcr.io/google-samples/gb-frontend:v6",
        "command" : [ ],
        "args" : [ ],
        "workDir" : null,
        "terminationMessagePath" : "/dev/termination-log",
        "terminationMessagePolicy" : "File",
        "imagePullPolicy" : "IfNotPresent",
        "stdin" : null,
        "stdinOnce" : null,
        "tty" : null,
        "ports" : [ {
            "id" : "964460ff-0508-432c-a0db-78390ab85e09",
            "service" : "Environments",
            "modelIndex" : "ContainerPort",
            "uri" : "/environments/api/containerPorts/964460ff-0508-432c-a0db-78390ab85e09"
        } ],
        "env" : [ {
            "id" : "d07dc2d5-d583-45f7-a05e-b9e249c94412",
            "service" : "Environments",
            "modelIndex" : "EnvVar",
            "uri" : "/environments/api/envVars/d07dc2d5-d583-45f7-a05e-b9e249c94412"
        } ],
        "volumeMounts" : [ {
            "id" : "87b4b177-88a7-4d2f-aaa1-622d4dd41ddf",
            "service" : "Environments",
            "modelIndex" : "VolumeMount",
            "uri" : "/environments/api/volumeMounts/87b4b177-88a7-4d2f-aaa1-622d4dd41ddf"
        } ],
        "livenessProbe" : [ ],
        "readinessProbe" : [ ],
        "lifecycle" : [ ],
        "resources" : [ {
            "id" : "1050e112-8898-4d57-8be6-f426f1905a90",
            "service" : "Environments",
            "modelIndex" : "ResourceRequirements",
            "uri" : "/environments/api/resourceRequirements/1050e112-8898-4d57-8be6-f426f1905a90"
        } ],
        "securityContext" : [ ]
    }
{{%/excerpt%}}
