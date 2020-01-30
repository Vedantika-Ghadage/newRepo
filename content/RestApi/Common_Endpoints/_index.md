+++
title = "Common Endpoints"
description = ""
weight=50
+++
{{%excerpt%}}
All resources implement a few common endpoints for querying related
resources:

##### descendants

Returns all descendants of a model type. The full URL is of the form:

    /{service}/api/{model}/{id}/descendants/{model}

Note that the *descendants* keyword is optional. So the following is an
equivalent query to retrieve all direct or sub-descendants:

    /{service}/api/{model}/{id}/{model}

##### ancestors

Returns all ancestors (parents and their parents) of a model instance.
The full URL is of the form:

    /{service}/api/{model}/{id}/ancestors

##### ancestor

Returns an ancestors of a model instance, that matches the provided
model type. The full URL is of the form:

    /{service}/api/{model}/{id}/ancestor/{model}

##### currentAlarms

Returns all current (active and not-cleared) alarms of a model instance:

    /{service}/api/{model}/{id}/currentAlarms

##### currentAlarmCounts

Returns the count of all current (active and not-cleared) alarms of a
model instance:

    /{service}/api/{model}/{id}/currentAlarmCounts
{{%/excerpt%}}
