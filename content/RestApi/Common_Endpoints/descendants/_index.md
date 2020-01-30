+++
title = "descendants"
description = ""
weight=10
+++
{{%excerpt%}}
Returns all descendants of a model type. The full URL is of the form:

    /{service}/api/{model}/{id}/descendants/{model}

Note that the *descendants* keyword is optional. So the following is an
equivalent query to retrieve all direct or sub-descendants:

    /{service}/api/{model}/{id}/{model}

{{%/excerpt%}}
