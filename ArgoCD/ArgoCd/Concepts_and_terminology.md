Target state: The desired state of the application, as represented by files in a git repository.
The live state: the live state of that application. What pods, configmap, secrets, etc are created and/deployed in a kubernetes cluster.
Sync status: Whether or not the live state matches the target state. Is the deployed application the same as Git says it should be?
Sync: The process of making an application move to its target state.E.g by applying changes to a kubernetes cluster.
Sync operation status: Whether or not sync succeeded.