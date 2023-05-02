# What is ArgoCD
Is a declarative, git ops continuous delivery tool for kubernetes resources defined in a Git repository.
Continuously monitors running applications and comparing their live state to the desired state.
It reports the deviation and provides visualizations to help developers manually or automatically sync the live state with the desired state.

# Why use ArgoCD

It extend the benefits of declarative specifications and git-based configuration management.
It is the first step in achieving continuous operations based on monitoring, analytics and automated remediation.
It can deploy to multiple clusters and is Enterprise-friendly (auditability, compliance, security, RBAC, SSO, and lot more).

# How ArgoCD works

It follow git ops pattern by using Git repositories as the source of truth for the desired state of app and the target deployment envs.
It supports many kubernetes manifest format.
Kustomize applications, Helm charts, Ksonnet applications, Jsonnet files, YAML/JSON manifests.
It automate the synchronization of the desired application state with each of the specified target environments.

