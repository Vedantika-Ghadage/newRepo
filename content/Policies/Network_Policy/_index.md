+++
title = "Network Policies"
description = ""
weight=50
+++
{{%excerpt%}}

Proper configuration management is an essential element of network security. In many enterprises, configuration management begins with robust network policies that control communication.

By default, when an application or workload run in a Kuberenetes cluster, everything in the cluster can communicate every pod in the cluster can talk to any other cluster. Pods are non-isolated. Pods can initiate and receive connections from internal and external pods.

Network policies allow you to control inbound (ingress) and outbound (egress) traffic within the cluster and are flexible. Network policies are configured based on flexors and require the support of a CNI such as:

* Calico
* Canal
* Cilium
* Kube-router
* Romana
* Weave Net

**NOTE:**  Network policies that are not supported by a CNI are not enforced.

A network policy definition is comprised of three parts:

1. Pod selector
2. Ingress block
3. Egress block

##### Pod Selector

A group of pods is selected through labels (such as application name).  The selected group of pods is isolated and explicit rules for allowed source, and destination communication are applied to the group.

##### Ingress and Egress Blocks

Ingress and egress blocks may be applied in any order. Multiple network policies can apply to the same group of pods by either grouping the policies together or by applying multiple policies to the same group of pods. When multiple policies are applied to the same group of pods, the least restrictive policy is used. For example, if one policy Allows Ingress and a second policy Blocks (Deny) Ingress, and both are applied to the same group of pods, Ingress will be allowed.

Each network policy rule is comprised of two parts:


1. NetworkPolicyPeer
2. NetworkPolicyPort

![image](/images/network-policy-1.png)

#### Network Policy Peer

The NetworkPolicyPeer is the other side of the connection. It could be configured through a CIDR notation that specifies IP address blocks, namespaces, or pod labels that may communicate with the pod group.

* If an IP Block is specified, the rule applies to the addresses defined by the block.
* If a Namespace is specified, the rule applies to select pods within the namespace.
* If a Namespace Selector is specified, the rule applies to all pods within a namespace.
* If a Pod and Namespace Selector is specified, the rule applies to select pods within a specified namespace.

IP Blocks and selectors cannot be combined within a rule. However, a policy can contain more than one rule.

#### How to Configure an IP Block

An IP Block must contain a CIDR address block (such as 10.10.1.1/16) and may contain an “exception” block (such as 10.10.1.1-32). Use the exception block to specify addresses to allow ingress sources or egress destinations. Note that the exception block must be a part of the specified CIDR range.

#### How to Configure Selectors

If a pod selector is specified, but no namespace selector the rule selects all pods in the current namespace.

If a namespace selector is specified, but no pod is selected, the rule selects all pods in the selected namespace.

If both a pod and a namespace are specified, the rule selects the specified pods and namespaces.

Note that “**all** pods in **all** namespaces” means all pods in the cluster and does not include external traffic.

#### Network Policy Port

**NetworkPolicyPort** allows you to explicitly name ingress and egress ports or protocols that may communicate with the pod group.

#### Best Practices for Default Policies

Since multiple policies can be applied to a group of pods, it is a best practice to define a default policy per a namespace and have it automatically is applied as namespaces are provisioned. To do so, use the Policy Engine in Nirmata, or other CM tool create a default policy that:

* Selects all pods: `podSelector: { }`
* Denys all egress: `egress: [ ]`
* Denys all ingress: `ingress: [ ]`

**Sample Default Policy that Selects all Pods, Denys all Egress, and Denys all Ingress:**

````
kind: NetworkPolicy
apiVersion:
networking.k8s.io/v1
metadata:
name: default-deny-all
namespace: somenamespace
spec:
policyTypes:
- Egress
- Ingress
podSelector: {}
egress: []
ingress: []
````

As a workload is configured, specify exclusions to the default policy in a separate policy. This policy can also include authorization controls.

**Sample Policy that Selects all Pods, Allows all Egress, and Denys all Ingress:**

```
kind: NetworkPolicy
apiVersion:
networking.k8s.io/v1
metadata:
name: default-deny-all
namespace: somenamespace
spec:
policyTypes:
- Egress
- Ingress
podSelector: {}
egress:
- {}
ingress: []
```

**NOTE:** An empty curly bracket { } selects everything. However, if the definition is not included in the policy or is included with empty square brackets [ ], it does not select anything.  

#### How to Manage Network Policies in Nirmata

Note that this demo uses Calico as the supporting CNI.

Managing Network Policies through Nirmata:

* Simplifies network policy configuration
* Centralizes configuration in the catalog
* Synchronizes catalog changes to running applications  

#### How to Create a New Network Policy in Nirmata

Navigate to *Catalog* in the sidebar menu, select *Applications*, and then open the application to which the network policy will apply.
Select the *Discovery & Routing* tab and then scroll down and select *Add a Network Policy*.

![image](/images/network-policy-2.png)

Name the Network Policy and then choose to apply it to *All* pods or specify pods.

![image](/images/network-policy-3.png)

The new Network Policy displays. Configure rules by clicking in the Ingress Rules and Egress Rules boxes.

#### How to Configure General Rules

Choose *Deny All* or *Allow All* under the Ingress and Egress Rules. Doing so denies or allows all traffic to the pod.

![image](/images/network-policy-4.png)

After configuring the policy, deploy the application by returning to the main Application screen and clicking *Run this application in an environment*. Enter a run name and select an environment and click *Run Application*.

![image](/images/network-policy-5.png)

![image](/images/network-policy-6.png)

The application deploys.

![image](/images/network-policy-7.png)

#### How to Configure Custom Rules

Choose to configure an ingress or egress rule and then select *Custom Rules* and choose *Allow Traffic*:

* From Pod Selector and Namespace Selector
* From IP Block
* From all destinations

![image](/images/network-policy-8.png)

If *From Pod Selector and Namespace Selector* is selected, the *Pod Selector and Namespace Selector* automatically populates with available deployments.

![image](/images/network-policy-9.png)

If *From IP Block* is selected, enter a CIDR address and then enter an Exception (as needed). Remember that the Exception must be contained within the CIDR block.

![image](/images/network-policy-10.png)

Then apply a *Protocol* and *Port*.

![image](/images/network-policy-11.png)

The new Network Policy rule is shown on the *Network Policy* page.

![image](/images/network-policy-12.png)

#### How to Export a Network Policy as a YAML

To export the Network Policy as a YAML for use in other areas of Kubernetes, open the application page and select *Export YAML* from the *Settings* menu.

![image](/images/network-policy-13.png)

Then choose the network policy and select *Download YAML file*.

![image](/images/network-policy-15.png)

#### How to Import a YAML File

To import a network policy as a YAML, open the application page and select *Import YAML* from the *Settings* menu.

Then search or drag and drop the YAML file into Nirmata.

![image](/images/network-policy-16.png)

{{%/excerpt%}}
