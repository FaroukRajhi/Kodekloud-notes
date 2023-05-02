
To follow this lab you will need an AWS account and associated credentials that allows you to create resources.


To use your IAM credentials to authenticate the Terraform AWS provider, set the AWS environment variable.

export AWS_ACCESS_KEY_ID=

export AWS_SECRET_ACCESS_KEY=

# Create a Terraform Cloud Workspace

Select New Workspace and choose the CLI-driven workflow

Name your workspace as devops-aws-myapp-dev
Provide a description: My Clumsy Bird Application - AWS - Development
Select Create Workspace

# Create Terraform Configuration



Let's deploy infrastructure using the Terraform Cloud workspace to store remote state.


To deploy the infrastructure for our application we will be using the Terraform configuration files present at /home/bob/clumsy-bird


Add a code block in backend.tf to set up the cloud integration.

# Deploy infrastructure using appropriate Terraform Cloud workspaces

terraform init

terraform plan

terraform apply

