+++
title = "Prometheus"
description = ""
weight=150
+++


#### Steps for Prometheus Deployment

Here are some key steps to deploying Prometheus - 



1. In your cluster, create an environment with nirmata-monitoring namespace.
2. Add prometheus-operator and Prometheus yaml’s provided.
3. Run prometheus-operator yaml in nirmata-monitoring environment
4. Run prometheus yaml in nirmata-monitoring environment.
5. Find the nodeport on which grafana service is exposed and access grafana dashboard on` http://<any of kubernetes master nodes>:NodePort`.
6. Access grafana using` admin/admin123`. You should see Kubernetes stats with pre-built dashboard.


#### Kubelet stats

For Nirmata provisioned cluster, you should start seeing all the stats. For base cluster, couple of configuration modifications are needed.



1. In the kubelet configuration file` /etc/systemd/system/kubelet.service.d/10-kubeadm.conf `- add following command - 


```
Environment="KUBELET_EXTRA_ARGS=--authentication-token-webhook --authentication-token-webhook=true --authorization-mode=Webhook
```


2. In the prometheus clusterrole, add following parameters - 

** kubectl edit clusterrole prometheus -n nirmata-monitoring **


```
- apiGroups:
  - ""
  resources:
  - nodes/metrics
  verbs:
  - get
```


You should start seeing kubernetes metrics.


#### Etcd stats

For etcd stats, we need to expose etcd as a service and create servicemonitor ( metrics exporter) for etcd. 

For an HA cluster, you need to expose all three etcd nodes as endpoints for the service. Here is yaml for exposing etcd as a service - 


```
apiVersion: v1
kind: Endpoints
metadata:
  name: etcd
  namespace: kube-system
subsets:
- addresses:
  - ip: 10.10.1.126
  - ip: 10.10.1.52
  - ip: 10.10.1.207
  ports:
  - name: https
    port: 2379
    protocol: TCP
---
apiVersion: v1
kind: Service
metadata:
  namespace: kube-system
  name: etcd
  labels:
    k8s-app: etcd
spec:
  type: ClusterIP
  clusterIP: None
  ports:
  - name: https
    port: 2379
    targetPort: 2379
    protocol: TCP


```


Now,we need to deploy the servicemonitor for etcd. You can use the yaml below - 


```
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: etcd
  namespace: nirmata-monitoring
  labels:
    k8s-app: etcd
spec:
  jobLabel: k8s-app
  selector:
    matchLabels:
      k8s-app: etcd
  namespaceSelector:
    matchNames:
    - kube-system
  endpoints:
  - port: https
    interval: 30s
    scheme: https
    tlsConfig:
      insecureSkipVerify: true
      caFile: /etc/prometheus/secrets/etcd-certs/ca.crt
      certFile: /etc/prometheus/secrets/etcd-certs/healthcheck-client.crt
      keyFile: /etc/prometheus/secrets/etcd-certs/healthcheck-client.key
```


For kubeadm provisioned base cluster, you may have insert etcd secrets in the servicemonitor as they  sit in a different directory.

To do this, create secrets from etcd certs using following command - 


<table>
  <tr>
   <td>
   </td>
  </tr>
  <tr>
   <td><code>`kubectl -n monitoring create secret generic etcd-certs --from-file=/etc/kubernetes/pki/etcd/healthcheck-client.crt --from-file=/etc/kubernetes/pki/etcd/healthcheck-client.key --from-file=/etc/kubernetes/pki/etcd/ca.crt'</code>
<p>
Once secrets are created, prometheus CRD needs to be updated - 
<p>
<code># kubectl edit prometheus prometheus -n nirmata-monitoring</code>
<p>
Add following under Spec:
<p>
<code>Secrets:</code>
<p>
<code>- etcd-certs</code>
<p>
You can use the etcd.json provided to import etcd dashboard and viola! , your etcd stats should be available.
   </td>
  </tr>
  <tr>
   <td>
   </td>
  </tr>
</table>
