Introduction
First, We need to install Packer and Terraform template to deploy a server in Azure.

Getting Started
Clone this repository

Create and assign custom policies using Azure CLI

Create create an image using Packer

Create infrastucture using Terraform

Dependencies
Create an Azure Account
Install the Azure command line interface
Install Packer
Install Terraform
Instructions
Create a custom policy definition
    az policy definition create --name "name" --rules "<path to .json file>"
Create a custom policy assignment
    az policy assignment create --name "name" --scope "subscription_id" --policy "<policy id>"
Use Azure CLI to create a Service Principal
    az ad sp create-for-rbac --role="Contributor" --scopes="subscription_id"
Set environment variables "TF_VAR_subscription_id" , "TF_VAR_client_id", "TF_VAR_client_secret" and "TF_VAR_tenant_id"

Use Packer to create the image

    packer build server.json
Use Terraform to create the infrastucture
    terraform init
    terraform plan --out solution.plan -var 'variable=varaible_value'
    terraform apply solution.plan 