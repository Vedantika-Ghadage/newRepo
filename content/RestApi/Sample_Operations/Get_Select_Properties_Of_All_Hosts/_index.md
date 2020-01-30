+++
title = "Get select properties of all hosts"
description = ""
weight=160
+++
{{%excerpt%}}
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

{{%/excerpt%}}
