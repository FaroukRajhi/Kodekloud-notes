Projects in OpenShift are the same, or very similar, to namespaces in Kubernetes.
When you deploy a Pod to OpenShift and you don’t specify a Project, it’ll be deployed to the default project
On the Pod section of the OpenShift UI, there’s a tab called Terminal so you can exec into the Pod
You can deploy standard Kubernetes Manifests to OpenShift
oc apply -f is the same as kubectl apply -f.






