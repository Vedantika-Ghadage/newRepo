+++
title = "Host Networking"
description = ""
weight=60
+++
{{%excerpt%}}

Nirmata does nor require any special networking setup, and works with
your existing Host networking. Nirmata uses the Docker bridge network
mode on each Host, so each application service is addressable using the
Host IP address and an allocated (static or dynamic) port. Based on the
cloud provider, Nirmata will detect the public and private IP addresses
of your Host. When available, the Host's private IP address will be
used for communication between services.
{{%/excerpt%}}
