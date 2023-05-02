It can be considered an extension of the Infrastructure as code IaC that uses git as the version control system.
The core idea is to have the infrastructure applications, and all related components declaratively defined in one or more Git repositories.
A GitOps operator runs within one of the kubernetes cluster, it continues monitors and pulls changes from git repository, that's mean trigger the changes.
It also updates the kubernetes manifest within another git repository.