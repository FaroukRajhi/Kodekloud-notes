Workspaces are how Terraform cloud tracks infrastructure.
Workspaces contain:
  - Linked VCS repository with terraform code.
  - Variables and values used by the configuration.
  - The current Terraform state file.
  - Historical states and run logs.

Separated workspace.

Workspace components:
state files.
variables.
operations and logs.
Notifications
Terraform version
Permissions
Cost Estimation
Policy enforcement
run history

Isolated environments with one state file.
Monolithic state file (Terraform OSS).

Reducing Blast Radius:
The ability to reuse code but limit the impact into a give component or into a given environment.
In Terraform Cloud, reducing blast radius refers to minimizing the impact of a potentially destructive change to your infrastructure by limiting the scope of the change. The blast radius is the area affected by a change, and reducing it means reducing the potential for unintended consequences.
One way to reduce blast radius in Terraform Cloud is to use workspaces. Workspaces are isolated environments that allow you to deploy changes to specific parts of your infrastructure without affecting other parts. For example, you might have a workspace for your development environment and a separate workspace for your production environment. If you make a mistake in your development environment, the blast radius is limited to that workspace, and your production environment remains unaffected.

Workspace naming
Names are important for organization, filtering and permissions.
syntax:

<app>-<tier>-<region>-<environment>
<team>-<environment>-<app>-<tier>-<region>-<#>

examples

eCommerce-web-us-west-1-prod
adt-mobile-qa-us-west-2-prod-002

Local execution

Terraform will no longer write to local .tfstate file.
Everything else about your local workflow remains the same.
Init, plan, apply is still the same, but now your state is stored on terraform cloud.
Your terraform configurations are still local.

Remote execution

init, plan, apply is still the same but your state is stored on terraform cloud.
Now you have more control with variables, policies, permissions, notifications.
Runs are happening IN Terraform Cloud.
  No longer dependable on local machine.
Historical view of all runs are now available in centralized location.
