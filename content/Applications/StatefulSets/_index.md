+++
title = "StatefulSets"
description = ""
weight=20
+++
{{%excerpt%}}
Some application components require stable identities e.g. distributed
software tools may require that cluster members retain the same names
and addresses within the cluster. Other software may manage large data
sets, requiring reusing the same volume. StatefulSets address solve of
these challenges, and provide additional controls over upgrades and
restarts suitable for stateful services.

As with a Deployment, StatefulSets also contain a Pod template and can
be referenced by a Service.
{{%/excerpt%}}
