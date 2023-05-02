# Enable Terraform Cloud Workspace for Remote Execution


We have our state in our Terraform Cloud workspace, we will begin to execute remote runs within the workspace.

Terraform operations like plan or apply can now be run within Terraform Cloud on a hosted agent, saving the results, and logs to the workspace.

Your team can review and collaborate on runs within the app.

It gives you a working environment for all Terraform runs and inspect logs when something goes wrong.


Navigate to Settings > General in Terraform Cloud Workspace.


Update the Execution Mode settings to Remote.

Update terraform variables file to work with remote execution


Terraform uses all Terraform and Environment variables for all plans and applies them in the workspace.

Workspaces using Terraform 0.10.0 or later loads default values from any *.auto.tfvars files in the configuration.


On your terminal, let's rename terraform.tfvars to terraform.auto.tfvars present in clumsy_bird directory.

