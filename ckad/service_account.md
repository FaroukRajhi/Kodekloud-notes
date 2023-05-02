Service accounts are used by machine.
a service account could be for an administrator accessing the cluster to perform administrative tasks or a developer accessing the cluster to deploy application etc.
a service account could be used by an application to interact with the kubernetes cluster.
For example, a monitoring application like prometheus uses a service account to pull the kubernetes API for performance metrics.
And Automated build tool like jenkins user service accounts to deploy application on the kubernetes cluster.
When the service account is created it also creates a token automatically.
The token is stored as a secret  linked to the service account.
We can copy the token when the service account is deployed.

# Update the deployment to use the newly created ServiceAccount

 spec:
      serviceAccountName: dashboard-sa
      containers:
      - image: gcr.io/kodekloud/customimage/my-kubernetes-dashboard
        imagePullPolicy: Always

