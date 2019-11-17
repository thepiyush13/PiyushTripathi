---
layout: post
title: Managing AWS infrastructure with Terraform
date: 2019-11-16 13:32:20 +0300
description: How to use terraform to deploy and manage AWS services # Add post description (optional)
img: icons/neutral_trading.svg #i-rest.jpg # Add image post (optional)
fig-caption: test caption # Add figcaption (optional)
tags: [terraform, aws]
---



# what is Terraform

Terraform is an open source tool which helps you deploy and manage infrastructure seamlessly across a veriety of providers. some of them are :

  

 1. Amazon Web Serv‐ices (AWS)
 2. Azure
 3. Google Cloud
 4. DigitalOcean

  

# Why Terraform

Writing infrstructeua as code is a powerful technuque. This mainly helps with the following:

 1. With code you can easily automate infra management
 2. reduce errors in complicated and time consuming configurations.
 3. do offline validation, diff or version control your changes
 4. let others resue your configuration easily

  

# Installing terraform
- Download the package from https://www.terraform.io/
- Add binary terraform to your PATH environment variable
- Setup Providers login details. For example setup AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY if you want to use terraform with AWS

  
  

# Using terraform

- Defining resources: create a file main.tf with the following 

    Simple syntex to use terraform is 

        resource "PROVIDER_TYPE" "NAME" {
            [CONFIG ...]
        }

    Example:

        resource "aws_instance" "test" {
            ami = "ami-xxxxx"
            instance_type = "t2.micro"
        }

- Creating resources: 
    Here we will try to create the actual resource
        
        terraform apply 
    
    (from folder where main.tf is)

- Destroying resources
        
        terraform destroy
    
    remove the created resource once no longer needed




  

# Terraform state files

  

# Terraform modules

  

# Terraform commands
    Usage: terraform [-version]  [-help]  <command>  [args]
    apply              Builds or changes infrastructure
    console            Interactive console for Terraform interpolations
    destroy            Destroy Terraform-managed infrastructure
    env                Workspace management
    fmt                Rewrites config files to canonical format
    get                Download and install modules for the configuration
    graph              Create a visual graph of Terraform resources
    import             Import existing infrastructure into Terraform
    init               Initialize a Terraform working directory
    output             Read an output from a state file
    plan               Generate and show an execution plan
    providers          Prints a tree of the providers used in the configuration
    push               Upload this Terraform module to Atlas to run
    refresh            Update local state file against real resources
    show               Inspect Terraform state or plan
    taint              Manually mark a resource for recreation
    untaint            Manually unmark a resource as tainted
    validate           Validates the Terraform files
    version            Prints the Terraform version
    workspace          Workspace management


# Terraform FAQS









