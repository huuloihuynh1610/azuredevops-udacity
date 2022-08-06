Introduction

    - To deploy a server to Azure Cloud using Packer image we need to install Packer & Terraform template the follow the step below.
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

Login to Azure

    az login 
Create a custom policy definition

    az policy definition create --name "name" --rules "server.json"
    ## Note:
        - server.json is the json file contain all your command to create packer image.
Create a custom policy assignment

    az policy assignment create --name "name" --scope "subscription_id" --policy "server.json"
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

To delete the source which is created, run this command:

    terraform destroy

Required variables are defined in variables.tf. Default values can be added to the file or value could be passed through cmdline when running terraform plan

    * prefix: The prefix for all resources in the template.
    * location: The Azure Region that we will use to deploy this resource.
    * source_image_name: The name of the source image was deployed by packer
    * source_image_rg: The name of the resource group of the image deployed by Packer
    * username: The username of the account of the VM(s)
    * password: The password of the account of the VM(s) (You can use ssh key for ubuntu, in this machine i used ssh key)
    * vm_machine_count: The number of virtual machines will be deployed.

Output

    - After runing all the commands you will see the messages on the command line, that is the result.
    - When you create the variable file you will see that the number of deployed resource is based on the number of vm_machine_count that you enter.