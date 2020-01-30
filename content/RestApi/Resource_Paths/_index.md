+++
title = "Resource Paths"
description = ""
weight=60
+++
{{%excerpt%}}
In some cases, identifying a resource requires information from multiple
objects. For example Deployments with the same name may exist in
different Applications. While an UUID can be used to identify the
resource, this is not very easy to use.

In these situations, A *Path* can be used to identify a resource
contained in a sub-tree. Each path element identifies a unique
Resource:

    "/" - Selects the root resource

    "/Entity[field=value, field=value]" - Selects a resource named 'Entity' queried by the field-value pairs

For example, suppose you have two Applications "Hello-World-1" and
"Hello-World-2", and each of these applications has a single
Deployment "hello". The following path will select the Deployment
"hello" in the Application "Hello-World-1":

    /applications/[name=Hello-World-1]/deployment[name=hello]

Since the Application "Hello-World-1" has a single service in it, the
path could also be written as:

    /application[name=Hello-World-1]/deployment

Paths can only be used when referring to a related resource (i.e. a
reference relationship) as an alternative to using the UUID for the
resource. In this form, a path is written as:

    {
        "id": "path:/application[name=Hello-World-1]/deployment"
        ...
    }

Another way to specify the path, instead of a string with the "path:"
prefix, is to use a JSON attribute:

    {
        "path": "/application[name=Hello-World-1]/deployment"
        ...
    }
{{%/excerpt%}}
