We have three  nodes.
We want to dedicate the data processing workloads to a specific pod.

First is using node selectors which is the simple and easier method.
in pod definition:
  nodeSelector:
    site: Large  (node label)
You must first label the node
kubectl label nodes <node-name> <label-key>=<label-value>
