Introduction
    - First, We need to install Packer and Terraform template to deploy a server in Azure.

Getting Started

    Clone this repository (https://github.com/huuloihuynh1610/azuredevops-udacity)

    Create and assign custom policies using Azure CLI

    Create create an image using Packer

    Create infrastucture using Terraform

Dependencies

    - Create an Azure Account
    - Install the Azure command line interface
    - Install Packer
    - Install Terraform
(Or you can run directly on Azure Clound Shell without install the tools above.)
    - Instructions
Create a custom policy definition

    az policy definition create --name "name" --rules "<path to .json file>"
Create a custom policy assignment

    az policy assignment create --name "name" --scope "subscription_id" --policy "<policy id>"
Use Azure CLI to create a Service Principal

    az ad sp create-for-rbac --role Contributor --scopes /subscriptions/<subscription_id> --query "{ client_id: appId, client_secret: password, tenant_id: tenant }"

    az account show --query "{ subscription_id: id }" ## use this command to show your subscription_id
Enter your SubscriptionId, ClientId, ClientSecret, TenantId into Server.json file.

Use Packer to create the image

    packer build server.json
Use Terraform to create the infrastucture

    terraform init

    terraform plan --out solution.plan -var 'variable=varaible_value'

    terraform apply solution.plan