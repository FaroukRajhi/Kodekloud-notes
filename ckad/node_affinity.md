The primary feature of the node affinity id to ensure the pods are hosted on particular nodes.
The node affinity feature provides us with advanced capabilities to limit pod placement on specific nodes.
Placed upon on the large node

affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoreDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: size
          operator: In
          values:
          - Large

The In operator insures that the pod will be placed on a node whose label size has any value in the list of values specified here.
we can add:

          values:
          - Large
          - medium

We can also prevent using NOT IN operator

      - matchExpressions:
        - key: size
          operator: NotIn
          values:
          - Small

Other operator is Exists:

      - key: size
          operator: Exists

It check if the label size exists on the nodes and you don't need the value section for that.
There many other operators check the documentation

# Node affinity types:

the node affinity type define the behavior of the scheduler with respect to node affinity and the stages in the lifecycle of the pod.

let's explain:

There are two states in the lifecycle of the pod when considering node affinity:

DuringScheduling: is the state where a pod does not exist and is created for the first time.
                  The affinity rules specified are consistent to place the pods on the right nodes
                  If you select the required type, which is the first one, the scheduler will mandate that the pod be placed on a node with the given affinity rules.
                  This type will be used in cases where the placement of the pod is crucial.

Type 2: 
preferredDuringSchedulingIgnoreDuringExecution:

DuringScheduling:
Preferred:
                The placement of the pod is less important.
                Where a matching node is not found.

The second part id DuringExecution:

Is the state where pod has been running and change is made in the environment that affects node affinity.
IgnoreDuringExecution: means pods will continue to run and any changes in node affinity will not impact them once they are scheduled.

The planned state:

requireDuringSchedulingRequireDuringExecution:

Will evict any pods that are running on nodes do not meet affinity rules.

# Set Node Affinity to the deployment to place the pods on node01 only.

 containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: color
                operator: In
                values:
                - blue

# Create a new deployment named red with the nginx image and 2 replicas, and ensure it gets placed on the controlplane node only.

Use the label key - node-role.kubernetes.io/control-plane - which is already set on the controlplane node.

 affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: node-role.kubernetes.io/control-plane
                operator: Exists