+++
title = "Operations"
description = ""
weight=20
+++
{{%excerpt%}}
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

{{%/excerpt%}}
