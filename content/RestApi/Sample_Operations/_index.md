+++
title = "Sample Operations"
description = ""
weight=70
+++
{{%excerpt%}}
##### Get all Catalog Applications

Request:

    GET /api/catalog/applications
    Accept: application/json
    Authorization: NIRMATA-API <key>

##### Get Deployment Details

The mode parameter is used to export all relations.

Request:

    GET /api/catalog/deployments/fbd5098b-a096-41f0-9f95-a012b9c86d96?mode=exportDetails
    Accept: application/json
    Authorization: NIRMATA-API <key>

##### Create an Application

Request:

    POST https://www.nirmata.io/api/applications/
    Accept: application/json
    Authorization: NIRMATA-API <key>

    {
        "name": "test-app",
    }

##### Delete an Application

Request:

    DELETE /api/catalog/applications/c7bf4bfa-346e-44f8-b62c-9b8fdf5c1980
    Accept: application/json
    Authorization: NIRMATA-API <key>

##### Get the UUID of an Application named 'helloworld' in YAML format

Request:

    GET /catalog/api/applications?query={"name": "helloworld"}&fields=id&output=YAML
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    ---
    - id: bdf910d6-f12d-4a9d-84e6-bfbae806c558

##### Get all running Applications' IDs, names, and states

Request:

    GET /environments/api/applications?fields=id,name,state
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [ {
    "id" : "76e72cd9-01dd-490e-be8b-a36951a21881",
    "name" : "nginx",
    "state" : "running",
    "run" : "nginx"
    }, {
    "id" : "97a1352d-4a0c-44b7-8ca6-0e264a203a59",
    "name" : "shopme",
    "state" : "running",
    "run" : "shopme"
    }, {
    "id" : "6a863004-02d7-4a64-85e6-004a140a5823",
    "name" : "aqua-csp",
    "state" : "running",
    "run" : "aqua-csp"
    }, {
    "id" : "bbab3d4f-17d7-45df-883a-e96d5a35def0",
    "name" : "shopmek8s",
    "state" : "running",
    "run" : "dealsapp"
    }, {
    "id" : "9b559b77-4d88-42ca-8280-5145ac3fe9f3",
    "name" : "shopmek8s",
    "state" : "running",
    "run" : "dealsapp"
    }, {
    "id" : "252cdc4b-69f2-4bb4-a688-170b95e516cc",
    "name" : "guestbook",
    "state" : "running",
    "run" : "guestbook"
    }, {
    "id" : "829e362c-cde2-4d06-b1c2-96bef10faed9",
    "name" : "guestbook",
    "state" : "running",
    "run" : "guestbook"
    }, {
    "id" : "343b46f2-6b93-45ac-b38b-bdbc2d133f1e",
    "name" : "guestbook",
    "state" : "running",
    "run" : "guestbook-2"
    } ]

##### Create a new Environment

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

##### Run an Application in an Environment

Request Headers:

    POST /catalog/api/applications/248ea469-50f2-4b8c-af55-f13a5527a356/run
    Accept: application/json
    Authorization: NIRMATA-API <key>

Request Body:

    {
      "run": "hello1",
      "environment": "dev-test"
    }

##### Find all Deployments and replica counts in running Applications

Request:

    GET /environments/api/applications?mode=exportDetails&fields=id,name,deployments,spec,replicas
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "76e72cd9-01dd-490e-be8b-a36951a21881",
            "name": "nginx"
        },
        {
            "id": "97a1352d-4a0c-44b7-8ca6-0e264a203a59",
            "name": "shopme",
            "deployments": [
                {
                    "id": "f23fb091-ec86-4b1c-aff9-744132d218b5",
                    "name": "payment",
                    "spec": [
                        {
                            "id": "8497448a-8cb0-4a38-9aac-ea941e226bce",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "00979b37-05be-4b09-b5c7-7af68cb7d0c6",
                    "name": "deals",
                    "spec": [
                        {
                            "id": "1d6ef0d7-91df-452c-b8af-ebf91f3e6b09",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "a01d5c5d-d5ae-4fc2-9fe9-6ee57ded98b0",
                    "name": "ratings",
                    "spec": [
                        {
                            "id": "8e0ed849-282a-40b0-8e7c-26ed7f4d8f26",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "6a863004-02d7-4a64-85e6-004a140a5823",
            "name": "aqua-csp",
            "deployments": [
                {
                    "id": "62a4ff2f-ad59-4479-9ba0-ee4104a13ce4",
                    "name": "aqua-all-in-one",
                    "spec": [
                        {
                            "id": "3ae07e78-0ae2-4672-b1df-56330a0c8b47",
                            "replicas": 1
                        }
                    ]
                }
            ]
        },
        {
            "id": "bbab3d4f-17d7-45df-883a-e96d5a35def0",
            "name": "shopmek8s",
            "deployments": [
                {
                    "id": "ec383532-8659-4a34-8d76-7eb5d85ffda3",
                    "name": "deals",
                    "spec": [
                        {
                            "id": "2da3cf04-2cee-4166-9491-566f5c9b3e27",
                            "replicas": 3
                        }
                    ]
                }
            ]
        },
        {
            "id": "9b559b77-4d88-42ca-8280-5145ac3fe9f3",
            "name": "shopmek8s",
            "deployments": [
                {
                    "id": "a9313032-1b82-40dd-b45a-4dabd0689102",
                    "name": "deals",
                    "spec": [
                        {
                            "id": "f9f861e8-defc-433c-b8f0-32c58d2a2fb1",
                            "replicas": 3
                        }
                    ]
                }
            ]
        },
        {
            "id": "252cdc4b-69f2-4bb4-a688-170b95e516cc",
            "name": "guestbook",
            "deployments": [
                {
                    "id": "27d56ae0-c58f-46a0-8b59-ca752f2fa109",
                    "name": "frontend",
                    "spec": [
                        {
                            "id": "ad1dcaf3-46fe-4c7d-8891-adfeadc1dc95",
                            "replicas": 3
                        }
                    ]
                },
                {
                    "id": "0b4f6d2e-28ac-4411-b98b-c9fe4875fc7d",
                    "name": "redis-master",
                    "spec": [
                        {
                            "id": "6f5659de-0a4c-4dbb-8baa-62a690d8538f",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "6d58b6cd-3179-4cdf-97f6-a273970540bf",
                    "name": "redis-slave",
                    "spec": [
                        {
                            "id": "7a01d526-0aaf-47ee-885d-b695a8ac8d2b",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "829e362c-cde2-4d06-b1c2-96bef10faed9",
            "name": "guestbook",
            "deployments": [
                {
                    "id": "1f539cf6-41cd-4739-8872-13409bba612d",
                    "name": "frontend",
                    "spec": [
                        {
                            "id": "32c81a2d-145f-4858-8be9-6669c2044079",
                            "replicas": 5
                        }
                    ]
                },
                {
                    "id": "8cd3b93e-2994-4f11-acef-5b4e830e252c",
                    "name": "redis-master",
                    "spec": [
                        {
                            "id": "87986a72-c250-4002-b4b6-c95cdada3b42",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "003bf3e2-065c-4a32-ac7b-fd2802e49a55",
                    "name": "redis-slave",
                    "spec": [
                        {
                            "id": "2069f1fd-1410-4569-9968-60cbabd140e1",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "343b46f2-6b93-45ac-b38b-bdbc2d133f1e",
            "name": "guestbook",
            "deployments": [
                {
                    "id": "50a1ed10-0167-4c8e-b8b1-a6319bef3cfb",
                    "name": "frontend",
                    "spec": [
                        {
                            "id": "576d2453-b139-4b38-a973-bda0afd9fa6c",
                            "replicas": 6
                        }
                    ]
                },
                {
                    "id": "cad14b31-7d14-46c1-81db-bb1430adb300",
                    "name": "redis-master",
                    "spec": [
                        {
                            "id": "de9d4e5e-f044-46b6-b147-2e9009c07f1b",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "0ef0caf9-b6ad-4a56-9f35-0e4c47a85627",
                    "name": "redis-slave",
                    "spec": [
                        {
                            "id": "1e487ab6-509a-4906-9717-49a2beb59cab",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "40d39730-ea05-4b0c-b78b-5d2d0008606b",
            "name": "dev-test2"
        }
    ]

##### Scale a Deployment in a running Application

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

##### Get the image versions for a container

Request:

    GET https://nirmata.io/environments/api/containers?fields=name,id,image&query={"name" : "php-redis"}
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "04c9ada6-8e62-408e-8bb7-4c5bc5e1db3b",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "1ca543fd-f406-4591-b786-382f8d34cac1",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "9f70e9b5-7aa0-4056-ac0a-1c4c6edb0c6b",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "53ac22ae-5d32-4341-bf19-fc2e3a27b4f4",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "24ae386e-ecc3-4b66-aab0-6e5364f06491",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "c4a11f29-48f1-4184-a05d-4f8d1a1760ab",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "e7f753f1-9ab6-458d-a743-3bf4f9b3e44e",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "40e95708-5bac-4b70-8591-7543aea01c6b",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "8cf514ca-f969-49f3-acc1-8d3dfbeef323",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "cd429f72-356e-41f6-b481-7c3cb1218b79",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "f33d7bb0-ecf3-403e-9d6f-5715bbe6cee4",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "97ca084f-e7cb-42c5-9b8b-f3d7f4c6914c",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "f4b0cb92-8aa6-4b5a-81a1-c51b7d0e3234",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "ffe03a27-be3f-4e81-b3f3-068bae378451",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "6b37a537-fce8-41f0-a5c1-bce980f23391",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "dbc0f31c-bc02-4a08-adb1-f994e9e130df",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "9bb53549-572c-499b-9bad-1d51079e13f2",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        }
    ]

##### Update image version for a running container

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

##### Select a PodTemplateSpec and output as YAML

Request:

    GET https://nirmata.io/environments/api/podTemplateSpecs?labelSelector="nirmata.io/environment.name=qa-environment,nirmata.io/application.run=guestbook,nirmata.io/component=redis-slave"&mode=export&output=yaml
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    Content-type: text/x-yaml;charset=UTF-8
    ...

Response Body:

    metadata:
    - labels:
        app: redis
        role: slave
        tier: backend
        nirmata.io/deployment.name: redis-slave
        nirmata.io/application.run: guestbook
        nirmata.io/environment.name: qa-environment
        nirmata.io/service.name: redis-slave
        nirmata.io/application.name: guestbook
        nirmata.io/component: redis-slave
    spec:
    - terminationGracePeriodSeconds: 30
      containers:
      - name: slave
        image: gcr.io/google_samples/gb-redisslave:v1
        ports:
        - containerPort: 6379
          protocol: TCP
        env:
        - name: GET_HOSTS_FROM
          value: dns

##### Apply YAML updates to a running Application

Request:

    curl -X POST -H "Content-type: text/yaml" -H "Authorization: NIRMATA-API $APIKEY" "https://nirmata.io/environments/api/applications/829e362c-cde2-4d06-b1c2-96bef10faed9/import" --data-binary @redis-slave.yml

Response:

    {
        "status" : 200,
        "message" : "Success",
        "changes" : {
            "user" : "jim@nirmata.com",
            "createdIds" : [ ],
            "modifiedIds" : [ {
            "modelIndex" : "Container",
            "uuid" : "1dff2449-a4f3-46a8-9b85-ad97eb0926d3",
            "service" : "Environments"
            } ],
            "deletedIds" : [ ],
            "sequenceId" : "dbe828e0-c079-4cc5-9562-f8c680fd8529",
            "timestamp" : 1526888853548,
            "empty" : false,
            "id" : "38c87ee5-0585-406e-82ac-5840551a8bef"
        }
    }

##### Get CPU and memory usage for all Clusters

Request:

    GET /cluster/api/hostClusters?mode=exportDetails&fields=id,name,kubernetesCluster,clusterStats,cpuUsagePercent,memoryUsagePercent
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "b33efdd1-7c10-4ca9-9c7d-a6e6baf65c4e",
            "name": "prod-cluster",
            "kubernetesCluster": [
                {
                    "id": "a6795f23-0801-4023-849c-9a7595e1e921",
                    "clusterStats": [
                        {
                            "id": "eafb354f-5c7e-4c6b-a6b7-e2ea0053c00f",
                            "cpuUsagePercent": 15.6,
                            "memoryUsagePercent": 59.060432
                        }
                    ]
                }
            ]
        },
        {
            "id": "fc91f1f5-6bb8-49d0-a506-cb770515a141",
            "name": "test-centos",
            "kubernetesCluster": [
                {
                    "id": "6619ae16-a8a0-4374-9ad7-baf5d0590f7d",
                    "clusterStats": [
                        {
                            "id": "6118e6dd-2536-43f7-9a79-1d2885a1aa7a",
                            "cpuUsagePercent": 8.175,
                            "memoryUsagePercent": 55.651302
                        }
                    ]
                }
            ]
        },
        {
            "id": "49202821-a458-45c8-8799-1a79e012471b",
            "name": "devtest-aks-us-east",
            "kubernetesCluster": [
                {
                    "id": "22259547-fd15-4a66-ba42-ae24ccb82563",
                    "clusterStats": [
                        {
                            "id": "286912b7-70ce-439e-8a59-0f51d9d2c0f4",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        },
        {
            "id": "f8aa846f-9c2d-4b2c-838f-23a8132ba78e",
            "name": "prod-azure-cluster",
            "kubernetesCluster": [
                {
                    "id": "3b026363-7f11-4ef7-a418-c8f73a34f6da",
                    "clusterStats": [
                        {
                            "id": "dbcea04b-7263-49b8-b9cd-f610782da5f0",
                            "cpuUsagePercent": 3.975,
                            "memoryUsagePercent": 13.631612
                        }
                    ]
                }
            ]
        },
        {
            "id": "cde8bdd5-37f4-445c-bf67-399fc22fffde",
            "name": "prod-aks-us-east2",
            "kubernetesCluster": [
                {
                    "id": "e8535a60-122a-41cc-9aac-b619dc3a3b8b",
                    "clusterStats": [
                        {
                            "id": "3ca358c1-c21a-43e1-a24a-770438515d57",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        },
        {
            "id": "933951fe-da2e-4bb1-a7d5-8dd092ff4ca2",
            "name": "aks-demo",
            "kubernetesCluster": [
                {
                    "id": "b4d8884d-e4c9-4881-8997-74b9a1bffa39",
                    "clusterStats": [
                        {
                            "id": "0dd79692-4ded-442d-a3a2-6519ee114901",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        },
        {
            "id": "c9bc4e81-4140-4120-afd1-4c8dc4b88574",
            "name": "diamanti-cluster-1",
            "kubernetesCluster": [
                {
                    "id": "c2d32dce-9e7b-4f03-9f2c-93936635c793",
                    "clusterStats": [
                        {
                            "id": "f21799b0-0ad7-40e3-a999-9c61fe022b00",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        }
    ]

##### Get select properties of all hosts

Request:

    GET https://nirmata.io/config/api/cloudProviders?fields=id,name,hostGroups,hosts,desiredCount,type,minHosts,maxHosts,type&mode=exportDetails
    Accept: application/json
    Authorization: NIRMATA-API <key>

Sample Response Body:

    [
        {
            "id": "a41f0493-f6e0-45d6-b56b-41ab93d9d392",
            "type": "Other",
            "name": "Direct Connect",
            "hostGroups": [
                {
                    "id": "2d6e6890-0c7a-4339-b6d0-8550fc98766b",
                    "name": "baremetal",
                    "desiredCount": 3,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "d5941122-8a9a-485f-a63a-f3b57bc220da",
                            "name": "baremetal-3"
                        },
                        {
                            "id": "edc8addf-756a-4427-9286-4f93aff2530a",
                            "name": "baremetal-2"
                        },
                        {
                            "id": "3901d892-b8c5-4495-a6e7-23bc71b9ba0a",
                            "name": "baremetal-1"
                        }
                    ]
                },
                {
                    "id": "f8f978db-8047-41db-95c4-dbab4501317c",
                    "name": "test-centos",
                    "desiredCount": 1,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "09fa7f0b-b06b-4f6d-a802-9013a16c731c",
                            "name": "ritesh-centos-92966"
                        },
                        {
                            "id": "b15a29f0-01b9-4986-bc60-da59f92ac5ab",
                            "name": "ritesh-centos-84460"
                        }
                    ]
                },
                {
                    "id": "efbe477f-7f18-40b2-87ec-a8078602fb30",
                    "name": "devtest-aks-us-east-hg",
                    "desiredCount": 1,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "68581e8b-66fc-4504-b8b2-00a763360dfb",
                            "name": "aks-nodepool1-14903811-0"
                        },
                        {
                            "id": "0338e6ec-2da7-4c92-9e47-0fa0601f065e",
                            "name": "aks-nodepool1-14903811-1"
                        }
                    ]
                },
                {
                    "id": "2226c92c-ff0f-4b71-88e6-5c85d079d4d3",
                    "name": "prod-aks-us-east2-hg",
                    "desiredCount": 1,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "f3dfab95-949c-4b17-8691-fbe45660b364",
                            "name": "aks-nodepool1-39911597-0"
                        },
                        {
                            "id": "0a1fd855-e942-4c9d-bdcd-d59c086f12d8",
                            "name": "aks-nodepool1-39911597-1"
                        }
                    ]
                },
                {
                    "id": "b4ff6180-b0e7-4951-a4cb-29572c481061",
                    "name": "aks-demo-hg",
                    "desiredCount": 1,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "9560d6e6-18ef-4087-9bf2-7981549d04e2",
                            "name": "aks-nodepool1-15724977-0"
                        },
                        {
                            "id": "5e7ccd73-a1e2-40b6-b0cc-2085fe8e8934",
                            "name": "aks-nodepool1-15724977-1"
                        }
                    ]
                }
            ]
        },
        {
            "id": "2e0c3c81-09ba-4633-b085-555040efc2dd",
            "type": "AWS",
            "name": "Nirmata-AWS",
            "hostGroups": [
                {
                    "id": "30fe5761-4ee6-45e4-b5ea-075cd91ae04b",
                    "name": "aws-demo",
                    "desiredCount": 0,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "9cfff737-b6fc-4512-8d4b-4eb3964361ed",
                            "name": "ip-10-10-131-70"
                        },
                        {
                            "id": "e1b514f1-ff4f-4df5-94f6-b0c1738c843e",
                            "name": "ip-10-10-130-51"
                        },
                        {
                            "id": "120fa82f-e70c-4d3f-b334-b06a9b655f98",
                            "name": "ip-10-10-130-190"
                        }
                    ]
                }
            ]
        },
        {
            "id": "45950d43-bac0-4ddb-9165-3fe91d3c0bc4",
            "type": "Azure",
            "name": "nirmata-azure",
            "hostGroups": [
                {
                    "id": "e3a14d35-5245-4acc-ad11-cfbb8a8a7cf3",
                    "name": "prod-hostgroup",
                    "desiredCount": 3,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "b3b26a3b-733d-4506-a6b0-629059ebeed9",
                            "name": "prod-hostgroup-72648"
                        },
                        {
                            "id": "b1f7c5ac-95ac-48ed-9c7e-67956db8c26b",
                            "name": "prod-hostgroup-35076"
                        }
                    ]
                },
                {
                    "id": "cb674cab-407d-48ef-924c-c83eb0379f00",
                    "name": "jim-prod-az",
                    "desiredCount": 3,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "f43145e8-cfb8-4bfc-ae31-69fdba133404",
                            "name": "jim-prod-az-12734"
                        },
                        {
                            "id": "7095c2af-8a51-4080-95bb-1f2d4ad107eb",
                            "name": "jim-prod-az-99904"
                        },
                        {
                            "id": "786b153f-8db0-41d7-9d6e-2963ad90f142",
                            "name": "jim-prod-az-11107"
                        }
                    ]
                }
            ]
        },
        {
            "id": "ebad7359-e4b3-4225-a6cc-0ababe1ae230",
            "type": "vSphere",
            "name": "vsphere-private-cloud",
            "hostGroups": [
                {
                    "id": "aec50dd9-64c5-4159-a9a5-dbe8ec079188",
                    "name": "vsphere-new-hg",
                    "desiredCount": 5,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "45ab49db-a32f-4aa3-93c1-12b10bc48df1",
                            "name": "vsphere-new-hg-44412"
                        },
                        {
                            "id": "3cc13241-2355-42f0-b912-87cdfd61a315",
                            "name": "vsphere-new-hg-68263"
                        },
                        {
                            "id": "71aa07a5-9f2e-4432-8bad-30724d0941b7",
                            "name": "vsphere-new-hg-23203"
                        },
                        {
                            "id": "f55d29f6-9855-4253-9f98-77e86b9eebd7",
                            "name": null
                        },
                        {
                            "id": "6bdb2cd2-4f8c-42fa-80b7-c36ece8a7cb6",
                            "name": "vsphere-new-hg-54753"
                        },
                        {
                            "id": "0e848355-1faa-4725-bb7a-4ee5aaceb694",
                            "name": "vsphere-new-hg-47703"
                        }
                    ]
                }
            ]
        },
        {
            "id": "b3c9bd96-48ce-4666-a5ed-46f08e06331a",
            "type": "Diamanti",
            "name": "Diamanti",
            "hostGroups": [
                {
                    "id": "08628b4c-703d-487b-adfb-2bb5c010e050",
                    "name": "diamanti-cluster-1-hg",
                    "desiredCount": 1,
                    "minHosts": 0,
                    "maxHosts": 5,
                    "hosts": [
                        {
                            "id": "c0ea5a98-a810-4082-a472-e153a2f8949b",
                            "name": "se21"
                        },
                        {
                            "id": "736ec330-fc5c-4ddf-90cb-a4d68507e2aa",
                            "name": "se22"
                        },
                        {
                            "id": "619e299a-403c-4e28-b2cc-ea4a769c6062",
                            "name": "se23"
                        }
                    ]
                }
            ]
        }
    ]

##### Create a new Kubernetes Cluster

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

##### Query a cluster's state

Request:

    GET https://nirmata.io/cluster/api/hostClusters?fields=id,state&query={"name" : "devtest-aks-us-east"}
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "49202821-a458-45c8-8799-1a79e012471b",
            "state": "ready"
        }
    ]

##### Discover the REST API schema

The Nirmata REST API schema can be queried using the HTTP OPTIONS
method. Here is a query and JQ filter to obtain all endpoints (model
classes):

Request:

    curl -X OPTIONS -H "Accept: application/json" -H "Authorization: NIRMATA-API <key>" https://nirmata.io/config/api | jq ".modelClasses | .[] .modelIndex"

Response:

    "Root"
    "Application"
    "EnvironmentType"
    "ContainerType"
    "ResourceSelectionPolicy"
    "ResourceSelectionRule"
    "CloudProvider"
    "HostGroup"
    "Host"
    "Container"
    "Service"
    "Environment"
    "ServiceInstance"
    "ServicePort"
    "ServiceSpec"
    "Registry"
    "LaunchConfiguration"
    "PortRange"
    "VSphereConfig"
    "OpenStackConfig"
    "WebHook"
    "ScalingPolicy"
    "DesiredService"
    "ScalingRule"
    "VCloudConfig"
    "ServiceInstanceAction"
    "ServiceAffinityRule"
    "ServiceScalingRule"
    "RoutingPolicy"
    "RoutingRule"
    "GatewayRoute"
    "GatewayPolicy"
    "GatewayRule"
    "AzureConfig"
    "DesiredServiceAction"
    "PrivateCloud"
    "CiscoIcfConfig"
    "CiscoUcsdConfig"
    "HealthCheck"
    "ClusterNode"
    "Cluster"
    "UpdatePolicy"
    "ImageUpdateEvent"
    "GatewayConfig"
    "ContainerAction"
    "DesiredServiceLabelSelector"
    "LabelSelectorItem"
    "EnvironmentVariable"
    "HostAction"
    "DigitalOceanConfig"
    "ProfitBricksConfig"
    "AwsConfig"
    "HostScalingRule"

##### Discover attributes and relations

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
