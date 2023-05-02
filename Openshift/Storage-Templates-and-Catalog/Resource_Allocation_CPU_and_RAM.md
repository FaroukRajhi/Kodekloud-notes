What pod can have?
Requests: it asks for a specific amount of CPU and Memory.
Requests without limits the pod keeps requesting CPU and memory.
Limits: Limiting the requests, the kubelet ensures that the limit is met.
We can add those parameters into deployment manifest file.
