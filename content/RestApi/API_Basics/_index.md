+++
title = "API Basics"
description = ""
weight=20
+++
{{%excerpt%}}
The Nirmata API model is composed of resources. Each resource type is
described by a class and is made up of *attributes* and *relations*.
Each resource has a *modelIndex* that indicates its class, and a *uri*
that describes how it can be queried. At runtime, each resource can
contain relations to other resources. The relations can be
*parent-child* relations or *reference* relations.

The Nirmata API is accessible at:

 <https://www.nirmata.io/api/>

**Note:** trying the API URL in a browser will return an empty page, as the
required HTTP headers are not specified. You can use a REST client, like
Postman (<http://www.getpostman.com/>), to try and learn the API.

##### Authentication

To authenticate your account, you can use HTTP BASIC authentication or
an API Key:

    Authorization BASIC <Bas64 user:password>

or:

    Authorization NIRMATA-API <your api key>

Since the Nirmata API is only accessible via HTTPS, your credentials are
sent over an encrypted connection.

To manage your API Key, login to Nirmata and navigate to *Settings ->
Account -> Generate API Key*. An API key is associated with a User
account. When you authenticate an application using the API key, it will
get the role and privileges associated with the account.

A best practice recommendation is to create separate accounts for each
application, and provide the minimum required role and privileges to the
account.

##### Operations

  Operation | HTTP Method | URI Syntax | Description
  ----------|-------------|------------|------------
  Create    | POST        | /{modelIndex} | Creates a new resource. The *modelIndex* is the resource name.
            |             |  /{parent}/{id}/{relation} | Create a new resource, as child of the '{parent}/{id}' resource
  Retrieve  | GET          | /{modelIndex}        |        Returns all resources of type specified by 'modelIndex'
            |               | /{modelIndex}/{id}  |        Returns a single resource
  Update    | PUT          | /{modelIndex}/{id}   |       Updates a resource
  Delete    |  DELETE      |  /{modelIndex}/{id}  |     Deletes a resource
  Discover  |  OPTIONS     | /                    |      Returns the class definitions for all resources
            |              | /{modelIndex}        |       Returns the class definition for a single resource

##### HTTP Response Status Codes

The following table lists common HTTP response codes used by the API:

  HTTP Status Code | Description
  ------------------|-----------------
  200      |         The operation succeeded
  401      |         The user authentication failed
  403      |         The request was not permitted
  406      |         The request results in an invalid configuration
  500      |         The request caused a server error

##### Resources

The following are some of the commonly used endpoints available via the
API:

 -   catalog/api/applications
 -   catalog/api/application/{id}/import
 -   catalog/api/application/{id}/export
 -   catalog/api/application/{id}/run
 -   catalog/api/deployments
 -   catalog/api/statefulSets
 -   catalog/api/podTemplateSpecs
 -   catalog/api/podSpecs
 -   catalog/api/volumes
 -   catalog/networkPolicies
 -   catalog/api/services
 -   catalog/api/ingresses
 -   catalog/api/configMaps
 -   catalog/api/secrets
 -   environments/api/environments
 -   environments/api/applications
 -   environments/api/application/{id}/import
 -   environments/api/application/{id}/export
 -   environments/api/deployments
 -   environments/api/statefulSets
 -   environments/api/podTemplateSpecs
 -   environments/api/podSpecs
 -   environments/api/volumes
 -   environments/networkPolicies
 -   environments/api/services
 -   environments/api/ingresses
 -   environments/api/configMaps
 -   environments/api/secrets
 -   environments/api/podSpecs
 -   environments/api/volumes
 -   environments/networkPolicies
 -   environments/api/services
 -   environments/api/ingresses
 -   environments/api/configMaps
 -   cluster/api/hostClusters
 -   cluster/api/nodes
 -   cluster/api/nodes
 -   cluster/api/events
 -   cluster/api/namespaces
 -   cluster/api/storageClasses
 -   cluster/api/persistentVolumes
 -   cluster/api/nodeStats
 -   cluster/api/clusterStats
 -   cluster/api/pendingPods
 -   cluster/api/clusterPolicies
 -   cluster/api/clusterRoles
 -   cluster/api/clusterRoleBindings
{{%/excerpt%}}
