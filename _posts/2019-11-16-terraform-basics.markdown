---
layout: post
title: Managing AWS infrastructure with Terraform
date: 2019-11-16 13:32:20 +0300
description: How to use terraform to deploy and manage AWS services # Add post description (optional)
img: icons/neutral_trading.svg #i-rest.jpg # Add image post (optional)
fig-caption: test caption # Add figcaption (optional)
tags: [Terraform, AWS]
---

# Table of Contents
{:toc}

# What is Terraform

Terraform is an open source tool which helps you deploy and manage infrastructure seamlessly across a variety of providers. some of them are :

  

 1. Amazon Web Services (AWS)
 2. Azure
 3. Google Cloud
 4. DigitalOcean

  

# Why Terraform

Writing infrastructure as code is a powerful technique. This mainly helps with the following:

 1. With code you can easily automate infra management
 2. reduce errors in complicated and time consuming configurations.
 3. do offline validation, diff or version control your changes
 4. let others reuse your configuration easily

  

# Installing Terraform
- Download the package from https://www.terraform.io/
- Add binary terraform to your PATH environment variable
- Setup Providers login details. For example setup AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY if you want to use terraform with AWS

  
  

# Using Terraform

- ## Defining resources: 

    create a file main.tf with the following 

    Simple syntax to use terraform is 

        resource "PROVIDER_TYPE" "NAME" {
            [CONFIG ...]
        }

    Example:

        resource "aws_instance" "test" {
            ami = "ami-xxxxx"
            instance_type = "t2.micro"
        }

- ## Creating resources: 
    Here we will try to create the actual resource
        
        terraform apply 
    
    (from folder where main.tf is)

- ## Destroying resources
        
        terraform destroy
    
    remove the created resource once no longer needed




  

# Terraform state files
Terraform maps the resources you defined in the template file to the resources it actually created in a JSON format. This file is called terraform state. This file resides in the same folder with the name `terraform.tfstate`. This state file is updated everytime you modify the resources. A good idea is to store this state file somewhere on S3 or a shared storage so everyone can work with the same state file and people do not end up with conflicting set of resources.
  

# Terraform modules
Terraform modules are the templates inside a folder. Modules are needed because they reduce code duplication and can work for multiple stages (dev, stage, prod). Terraform modules have three parts:
To understand this we need to think of terraform modules as functions in a programming language. Each function has input,output and actions. so for terraform:

    (input + definition + output) = Terraform module 

## Input : 
These are the parameters a module can accept while being called. They are defined in a `vars.tf` file inside the module folder. They can be of type bool, number or string. Inputs make a module more flexible as we can change the way the module behaves just by changing the inputs to the module. 

## Definition : 
The module file `main.tf` has the definitions of the various actions our module will perform. This file is considered the source of any terraform module. This file can be sourced from any external module to call this module. 

## Output : 
These are the variables terraform produces when it executes the actions defined in `main.tf`. These variables are defined in `output.tf` file in the module folder. These variable can give you back important information about the state of the resources, i.e. getting a instance ID after creating an EC2 instance. 


## Example
**We will create a module to create a resource and call this module from another module.**

* create a folder `my_module` and create files `vars.tf`, `output.tf` and `main.tf` inside it
* inside the vars.tf
        variable "type" {
            description = "type of instance"
        }
*  Inside the main.tf:
        resource "aws_instance" "test" {
            ami = "i-xxxx"
            instance_type = "${var.type}"
        }
* Inside the output.tf:
        output "name" {
            value = "${aws_instance.test.name}"
        }
* Now to call this module:
        module "my_module" {
            source = "modules/my_module"
            type =   "t2.micro"
        }
if you want to access the name of the created resource, you could do `${module.my_module.name}`


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

## What is terraform interpolation?
interpolation is used if you want to use dynamic values or refer to expressions within terraform. it is wrapped in ${}. For example `${var.foo}` or `${var.myArray['foo']}` and `${var.count+1}` are all examples of interpolation. You can find out more about it [here](https://www.terraform.io/docs/configuration-0-11/interpolation.html)

## what are terraform variables?
Read section `Terraform modules > Input` section above for details about input variables.

## what are terraform providers?
Providers are the infrastructure services that terraform is compatible with. Terraform supports a number of providers: AWS, GCP, Microsoft Azure, OpenStack, Heroku, DNSimple, CloudFlare. See [here](https://www.terraform.io/docs/providers/index.html) for more details.

## How to create an aws lambda with terraform?
    resource "aws_lambda_function" "my_lambda" {
    filename      = "lambda_file.zip"
    function_name = "function_name"
    role          = "<setup your IAM role here>"
    handler       = "exports.test"
    source_code_hash = "${filebase64sha256("lambda_file.zip")}"

    runtime = "nodejs8.10"

    environment {
        variables = {
        key1 = "val1"
        }
    }
    }

## How to create a dynamodb table from with terraform?
    resource "aws_dynamodb_table" "test-table" {
    name           = "test"
    billing_mode   = "PROVISIONED"
    read_capacity  = 5
    write_capacity = 5
    hash_key       = "ID"
    range_key      = "Email"

    attribute {
        name = "ID"
        type = "S"
    }

    attribute {
        name = "Email"
        type = "S"
    }

    tags = {
        Name        = "dynamodb"
        Environment = "production"
    }
    }


**Tags**
install terraform,terraform lambda,terraform vs ansible,terraform interpolation,terraform variables,terraform remote state,terraform providers,terraform vs cloudformation,terraform output,terraform registry,terraform workspaces,terraform locals,terraform vpc module,terraform dynamodb,terraform kubernetes,terraform iam role




