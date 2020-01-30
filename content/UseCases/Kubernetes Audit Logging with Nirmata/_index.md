+++
title = "Kubernetes Audit Logging with Nirmata"
description = ""
weight=170
+++




#### Audit Logging on Kubernetes


Set the parameters for apiserver, pass the file path for the audit log yaml inside the container(can be any path you want)


![image](/images/Audit-Logging0.png)


- Create a cluster using your custom cluster policy

- While cluster is deploying, go to this page by clicking on `view details` of components (double gear icon)



![image](/images/Audit-Logging1.png)


Click on the second `settings` icon from the top, you will see components details, find the `volumes` chart



![image](/images/Audit-Logging2.png)


Click `edit`  for apiserver, specify the folder you want to mount to this container


![image](/images/Audit-Logging3.png)


Redeploy apiserver, this path will mount to the container and you can load the audit policy.

By exec into the kubeapi you can now tail the kube-audit log we have created.


![image](/images/Audit-Logging4.png)



