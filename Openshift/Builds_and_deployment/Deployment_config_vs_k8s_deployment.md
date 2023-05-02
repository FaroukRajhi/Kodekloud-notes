Inside of kubernetes you have deployments or your deployments controller and that's what actually creates pods.
In openshift you have deployments and you also have the deployment config.
Check out the documentation , Also there is no much difference between them:
For example apiVersion in k8s : apps/v1, in openshift: apps.openshift.io/vs
kind in k8s : Deployment
kind in openshift: DeploymentConfig.
openshift: replica controller
k8s: replica set.
