+++
title = "Create a new Kubernetes Cluster"
description = ""
weight=170
+++
{{%excerpt%}}
Request:

    POST /api/cluster/hostClusters
    Accept: application/json
    Authorization: NIRMATA-API <key>

    {
        "name": "<name>",
        "mode" : "managed",
        "policySelector" : "<policy name>",
        "hostGroupSelector": {
            "matchLabels": {
                "name": "<host group name>"
            }
        }
    }

Sample Response Body:

    {
    "id" : "47870870-3a08-4a2b-991a-a028be7272f0",
    "service" : "Cluster",
    "modelIndex" : "HostCluster",
    "uri" : "/cluster/api/hostClusters/47870870-3a08-4a2b-991a-a028be7272f0",
    "parent" : {
        "id" : "4bf122ed-68d8-4d98-a3de-7ec2a6f766c8",
        "service" : "Cluster",
        "modelIndex" : "Root",
        "uri" : "/cluster/api/roots/4bf122ed-68d8-4d98-a3de-7ec2a6f766c8",
        "childRelation" : "hostClusters"
    },
    "createdBy" : "jim@nirmata.com",
    "createdOn" : 1526779036404,
    "modifiedBy" : "jim@nirmata.com",
    "modifiedOn" : 1526779036404,
    "generation" : 0,
    "ancestors" : [ {
        "uuid" : "4bf122ed-68d8-4d98-a3de-7ec2a6f766c8",
        "modelIndex" : "Root",
        "service" : "Cluster"
    } ],
    "labels" : {
        "nirmata.io/hostcluster.name" : "my-cluster"
    },
    "additionalProperties" : { },
    "alarms" : [ ],
    "name" : "my-cluster",
    "orchestrator" : "kubernetes",
    "state" : "pendingCreate",
    "mode" : null,
    "status" : [ ],
    "action" : null,
    "hostGroups" : [ {
        "service" : "config",
        "modelIndex" : "HostGroup",
        "id" : "30fe5761-4ee6-45e4-b5ea-075cd91ae04b"
    } ],
    "environments" : null,
    "clusterEnvironment" : null,
    "isDefaultCluster" : null,
    "connectionState" : "notConnected",
    "executionState" : null,
    "hostGroupSelector" : {
        "matchLabels" : {
        "name" : "aws-demo"
        },
        "matchExpressions" : [ ]
    },
    "notConnectedSince" : 1526779036405,
    "policySelector" : null,
    "description" : null,
    "adminState" : "enabled",
    "isAutoscalable" : null,
    "createDefaultEnvironment" : true,
    "isInitialized" : false,
    "lastSyncTime" : null,
    "volumes" : [ ],
    "kubernetesCluster" : [ {
        "id" : "8340a831-b805-4a01-9fc5-d14a673f56a7",
        "service" : "Cluster",
        "modelIndex" : "KubernetesCluster",
        "uri" : "/cluster/api/kubernetes/8340a831-b805-4a01-9fc5-d14a673f56a7"
    } ],
    "systemTasks" : [ ]
    }
{{%/excerpt%}}
