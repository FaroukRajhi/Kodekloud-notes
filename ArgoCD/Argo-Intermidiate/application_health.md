ArgoCD continuously check the status of kubernetes resources.
Let's assume argo CD has pulled a deployment manifest and applied it on a kubernetes cluster.
Argo CD will monitor this deployment and designate it as unhealthy if it is unable to scale up to the necessary number of replicas.
There are health checks:

* Health status: used when all the resources are 100% healthy.
* Progressing status is used if a resource is unhealthy but could still be healthy given time.
* Degraded status is used if the resource status indicates a failure.
* Missing status is used if resource is not present in cluster.
* Suspended status is used if the resource is suspended or paused.
* Unknown: if a health assessment failed and actual health status is not known.

We can custom the application health check.
Custom health checks can be defined in Argo CS configMap.
