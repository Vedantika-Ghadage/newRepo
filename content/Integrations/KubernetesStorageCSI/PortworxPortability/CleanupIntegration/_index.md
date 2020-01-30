+++
title = "Clean Up Integration"
description = ""
weight=90
+++
{{%excerpt%}}

Delete the secret for MySQL by entering the Delete Secret for MySQL command in the terminal window.

**Delete Secret for MySQL Command:**
```
kubectl delete secret mysql-pass
```

Delete WordPress by entering the Delete WordPress command in the terminal window.

**Delete WordPress Command:**
```
kubectl delete -f wordpress-deployment.yaml
kubectl delete -f wordpress-vol.yaml
```

Delete MySQL for WordPress by entering the Delete MySQL for WordPress command in the terminal window.

**Delete MySQL for WordPress Command:**
```
kubectl delete -f mysql.yaml
kubectl delete -f mysql-vol.yaml
```

Note: Portworx PersistentVolume allows for the creation of the Deployments and Services at this point without losing data. However, the hostPath will lose the data as soon as the Pod stops running.


{{%/excerpt%}}