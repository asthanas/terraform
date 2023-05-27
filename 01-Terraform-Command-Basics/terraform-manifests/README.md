---
title: Terraform Command Basics
description: Learn Terraform Commands like init, validate, plan, apply and destroy
---

## Step-01: Introduction
- Understand basic Terraform Commands
1. terraform init
2. terraform validate
3. terraform plan
4. terraform apply
5. terraform destroy      

[![Image](https://stacksimplify.com/course-images/azure-terraform-workflow-1.png "HashiCorp Certified: Terraform Associate on Azure")](https://stacksimplify.com/course-images/azure-terraform-workflow-1.png)

[![Image](https://stacksimplify.com/course-images/azure-terraform-workflow-2.png "HashiCorp Certified: Terraform Associate on Azure")](https://stacksimplify.com/course-images/azure-terraform-workflow-2.png)

## Step-02: Review terraform manifests
- **Pre-Conditions-1:** Get Azure Regions and decide the region where you want to create resources
```t
# Get Azure Regions
az account list-locations -o table
```
- **Pre-Conditions-2:** If not done earlier, complete `az login` via Azure CLI. We are going to use Azure CLI Authentication for Terraform when we use Terraform Commands. 
```t
# Azure CLI Login
az login

# List Subscriptions
az account list

# Set Specific Subscription (if we have multiple subscriptions)
az account set --subscription="SUBSCRIPTION_ID"
```
- [Azure Regions](https://docs.microsoft.com/en-us/azure/virtual-machines/regions)
- [Azure Regions Detailed](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions#what-are-paired-regions)
```t
# Terraform Settings Block
terraform {
  required_version = ">= 1.0.0"
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = ">= 2.0" # Optional but recommended in production
    }    
  }
}
# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
# Create Resource Group 
resource "azurerm_resource_group" "my_demo_rg1" {
  location = "eastus"
  name = "my-demo-rg1"  
}
```

## Step-03: Terraform Core Commands
```t
# Terraform Initialize
terraform init

# Terraform Validate
terraform validate

# Terraform Plan to Verify what it is going to create / update / destroy
terraform plan

# Terraform Apply to Create Resources
terraform apply 
```

## Step-04: Verify Azure Resource Group in Azure Management Console
- Go to Azure Management Console -> Resource Groups 
- Verify newly created Resource Group
- Review `terraform.tfstate` file 

## Step-05: Destroy Infrastructure
```t
# Destroy Azure Resource Group 
terraform destroy
Observation:
1. Verify if the resource group got deleted in Azure Management Console
2. Verify terraform.tfstate file and resource group info should be removed
3. Verify terraform.tfstate.backup, it should have the resource group info here stored as backup. 

# Delete Terraform files 
rm -rf .terraform*
rm -rf terraform.tfstate*
```

## Step-08: Conclusion
- Re-iterate what we have learned in this section
- Learned about Important Terraform Commands
1. terraform init
2. terraform validate
3. terraform plan
4. terraform apply
5. terraform destroy      
 
Execution : 

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/azurerm versions matching ">= 2.0.0"...
- Installing hashicorp/azurerm v3.58.0...
- Installed hashicorp/azurerm v3.58.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```t
saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ ls -alrt
total 5
drwxr-xr-x 1 saura 197609    0 May 20 11:39 ../
-rw-r--r-- 1 saura 197609  452 May 20 11:39 azure-resource-group.tf
drwxr-xr-x 1 saura 197609    0 May 27 13:01 .terraform/
-rw-r--r-- 1 saura 197609 1187 May 27 13:01 .terraform.lock.hcl
drwxr-xr-x 1 saura 197609    0 May 27 13:01 ./
```

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ cat .terraform.lock.hcl

# This file is maintained automatically by "terraform init".
# Manual edits may be lost in future updates.
provider "registry.terraform.io/hashicorp/azurerm" {
  version     = "3.58.0"
  constraints = ">= 2.0.0"
  hashes = [
    "h1:ceZlVBDs02TjOxY4JGLaeqCigsy7gcEPLcJudiTurb4=",
    "zh:22b19802605ca3e2b811e33650438be3647748cf8f75474c78448c30ac1cad0b",
    "zh:402ce010f4b68337abaccf8059c37294cabcbdbc3cefd9491dcd312e36ceea3c",
    "zh:53d2cd15f1631c7ffb47918064d644899cc671d47c72f4dafee4e2a5e69afd14",
    "zh:5a6b1c55629cff555472d1d43ad6e802693f7fd046c7d37718d4de6f52dbf66b",
    "zh:6181dccb7bca7cd84b0295a0332f19a7347a9586101f0a5e51b53bda1ec74651",
    "zh:854181d6a8821b3707775c913e91dd7944fcb55098953ef030168fa3cd0224aa",
    "zh:b44c758424d1a037fd833e0c69b29e3ac4047ab95653bb3e080835e55bd9badb",
    "zh:b6ee916a1579bba29b1aacce8897c6733fa97ba0dba2808f1ffa9ab492743fab",
    "zh:b7ab57044649578410dadfdf4412fc5f8aa085a25ea0b061393e843b49b43b63",
    "zh:cb68ddb922eb4be74dedf58c953d7f778b4e5f3cdcbe2ea83e02b12296ce4969",
    "zh:f569b65999264a9416862bca5cd2a6177d94ccb0424f3a4ef424428912b9cb3c",
    "zh:fe9e86173134cd9dc8ed65eae8634abc6d6f6806b5b412f54fccf4047052daa0",
  ]
}


saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ cd .terraform

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform (main)
$ ls -alrt
total 0
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ./
drwxr-xr-x 1 saura 197609 0 May 27 13:01 providers/
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ../

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform (main)
$ cd providers/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers (main)
$ ls -alrt
total 0
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ../
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ./
drwxr-xr-x 1 saura 197609 0 May 27 13:01 registry.terraform.io/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers (main)
$ cd registry.terraform.io/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io (main)
$ ls -alrt
total 0
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ../
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ./
drwxr-xr-x 1 saura 197609 0 May 27 13:01 hashicorp/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io (main)
$ cd hashicorp/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io/hashicorp (main)
$ ls -alrt
total 0
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ../
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ./
drwxr-xr-x 1 saura 197609 0 May 27 13:01 azurerm/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io/hashicorp (main)
$ cd azurerm/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io/hashicorp/azurerm (main)
$ ls -alrt
total 0
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ../
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ./
drwxr-xr-x 1 saura 197609 0 May 27 13:01 3.58.0/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io/hashicorp/azurerm (main)
$ cd 3.58.0/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io/hashicorp/azurerm/3.58.0 (main)
$ ls -alrt
total 0
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ../
drwxr-xr-x 1 saura 197609 0 May 27 13:01 ./
drwxr-xr-x 1 saura 197609 0 May 27 13:01 windows_386/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io/hashicorp/azurerm/3.58.0 (main)
$ cd windows_386/

saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests/.terraform/providers/registry.terraform.io/hashicorp/azurerm/3.58.0/windows_386 (main)
$ ls -alrt
total 179016
drwxr-xr-x 1 saura 197609         0 May 27 13:01 ../
drwxr-xr-x 1 saura 197609         0 May 27 13:01 ./
-rwxr-xr-x 1 saura 197609 183310336 May 27 13:01 terraform-provider-azurerm_v3.58.0_x5.exe*


saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ terraform plan

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.my_demo_rg1 will be created
  + resource "azurerm_resource_group" "my_demo_rg1" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "my-demo-rg1"
    }

Plan: 1 to add, 0 to change, 0 to destroy.

─────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't
guarantee to take exactly these actions if you run "terraform apply" now.




saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ terraform apply

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.my_demo_rg1 will be created
  + resource "azurerm_resource_group" "my_demo_rg1" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "my-demo-rg1"
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

azurerm_resource_group.my_demo_rg1: Creating...
azurerm_resource_group.my_demo_rg1: Still creating... [10s elapsed]
azurerm_resource_group.my_demo_rg1: Creation complete after 15s [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.


saura@DESKTOP-R7PUA66 MINGW64 /d/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ ls -alrt
total 14
drwxr-xr-x 1 saura 197609    0 May 20 11:39 ../
drwxr-xr-x 1 saura 197609    0 May 27 13:01 .terraform/
-rw-r--r-- 1 saura 197609 1187 May 27 13:01 .terraform.lock.hcl
-rw-r--r-- 1 saura 197609  432 May 27 14:28 azure-resource-group.tf
-rw-r--r-- 1 saura 197609  180 May 27 15:14 terraform.tfstate.backup
-rw-r--r-- 1 saura 197609  945 May 27 15:14 terraform.tfstate
drwxr-xr-x 1 saura 197609    0 May 27 15:14 ./



saura@DESKTOP-R7PUA66 MINGW64 /d/Udemy/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ terraform destroy
azurerm_resource_group.my_demo_rg1: Refreshing state... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1]

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # azurerm_resource_group.my_demo_rg1 will be destroyed
  - resource "azurerm_resource_group" "my_demo_rg1" {
      - id       = "/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1" -> null
      - location = "eastus" -> null
      - name     = "my-demo-rg1" -> null
      - tags     = {} -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

azurerm_resource_group.my_demo_rg1: Destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 10s elapsed]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 20s elapsed]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 30s elapsed]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 40s elapsed]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 50s elapsed]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 1m0s elapsed]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 1m10s elapsed]
azurerm_resource_group.my_demo_rg1: Still destroying... [id=/subscriptions/6c6cba0c-3a28-4ff5-8ac5-3f9453325ec5/resourceGroups/my-demo-rg1, 1m20s elapsed]
azurerm_resource_group.my_demo_rg1: Destruction complete after 1m25s

Destroy complete! Resources: 1 destroyed.


saura@DESKTOP-R7PUA66 MINGW64 /d/Udemy/terraform/terraform-on-azure-cloud/03-Terraform-Command-Basics/terraform-manifests (main)
$ rm -rf .terraform*
$ rm -rf terraform.tfstate*
