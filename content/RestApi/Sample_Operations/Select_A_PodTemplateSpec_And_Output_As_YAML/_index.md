+++
title = "Select a PodTemplateSpec and output as YAML"
description = ""
weight=130
+++
{{%excerpt%}}
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

{{%/excerpt%}}
