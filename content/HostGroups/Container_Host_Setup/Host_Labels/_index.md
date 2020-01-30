+++
title = "Host Labels"
description = ""
weight=30
+++
{{%excerpt%}}
You can setup host labels when installing the Nirmata agent. Nirmata
agent can detect host labels directly from Docker Engine. Host labels
can also be passed in to Nirmata agent using environment variables.

Docker Engine:

Add the label option when start Docker Engine. Depending on your docker-engine installation, you can add the label option to DOCKER_OPTS  

e.g. --label environment-type="production"

Environment variable:

You can add the labels to Nirmata agent as environment variables. For this, you can modify the Nirmata agent init script (/etc/init/nirmata-agent.conf) and update the HOST_LABELS field. The labels should be specified in json format without any whitespaces.

e.g. HOST_LABELS={"host-type":"SSD","host-location":"us-east"}

Once you setup the host labels, you will need to restart the Nirmata
agent. The host labels should be detected and display in Nirmata console
once the host connects. Now, you can use these labels to control the
placement of your containers.
{{%/excerpt%}}
