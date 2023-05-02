All about to restrict what pods are placed on what nodes.
Taints and toleration are used to set restrictions on what pod can be scheduled on a node.
Let us started with a simple cluster with three worker nodes.
The nodes are named one, two, and three.
We also have a set of pods that are to be deployed on these nodes.
Lets call them A,B,C and D.

First we prevent all pods from being placed on the node by placing a taint on the node, lets call it blue.
By default pods have no toleration: none of the pod can tolerate the taint.
in this case none of the pods can be placed on nodes one (tainted).
No unwanted pods are going to be placed on this node.

For this we must specify which pods are tolerant to this particular taint.
We want to allow pod D to be tolerant and add it to pod.
Node can be accept pod D.

# How to use this

kubectl taint nodes node-name key=value:taint-effect. 
key=value : in the pod should be the same.
taint-effect: what happens to POD that DO NOT TOLERATE this taint?
There are three types of taints:
  - NoSchedule : which means the pods will not be scheduled on the node.
  - PreferNotSchedule : which means the system will try to avoid placing a pod on the node but that's not guaranteed.
  - NoExecute : which means that new pods will not be scheduled on the node and existing pods on the node if any will be evicted of they do not tolerate the taint.

e .g 

kubectl taint nodes node1 app=blue:NoSchedule

Toleration added to pod, to add a toleration to a pod pull the pod definition yaml:
  - in spec section called toleration and move the key value
    tolerations:
    - key: "app""
      operator: "="
      value:""" blue"
      effect: ""NoSchedule""
