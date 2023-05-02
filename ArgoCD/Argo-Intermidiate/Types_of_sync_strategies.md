When ArgoCD discovers a new version of your application in Git, it either performs a manual sync or an automated sync.
If set to automatic, Argo CD will apply the changes then update or create new resources in the target kubernetes cluster.
If it is set to manual, Argo CD will delete the changes, but it won't make any changes to the cluster until and unless a user manually clicks on the sync button within the UI or CLI.
Auto-pruning of resources: Feature describes what happens when files are detected or removed from Git.Argo won't delete anything from the cluster if this feature is disabled.
Self-healing of cluster: Defines what argo does when you make kubectl edit changes directly to the cluster.