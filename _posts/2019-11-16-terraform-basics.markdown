---
layout: post
title: Managing AWS infrastructure with Terraform
date: 2019-11-16 13:32:20 +0300
description: How to use terraform to deploy and manage AWS services # Add post description (optional)
img: icons/neutral_trading.svg #i-rest.jpg # Add image post (optional)
fig-caption: test caption # Add figcaption (optional)
tags: [terraform, aws]
---



# what

Terraform is an open source tool which helps you deploy and manage infrastructure seamlessly across a veriety of providers. some of them are :

  

 1. Amazon Web Serv‐ices (AWS)
 2. Azure
 3. Google Cloud
 4. DigitalOcean

  

# Why

Writing infrstructeua as code is a powerful technuque. This mainly helps with the following:

 1. With code you can easily automate infra management
 2. reduce errors in complicated and time consuming configurations.
 3. do offline validation, diff or version control your changes
 4. let others resue your configuration easily

  

# Installing terraform

  
  

# Using terraform

- Creating resources

- Destroying resources



  

# Terraform state files

  

# Terraform modules

  

# Terraform commands

  

- ## All Commands

    Usage: terraform [-version]  [-help]  <command>  [args]
    
      
    
    The available commands for execution are listed below.
    
    The most common, useful commands are shown first, followed by
    
    less common or more advanced commands. If you're just getting
    
    started with Terraform, stick with the common commands. For the
    
    other commands, please read the help and docs before usage.
    
      
    
    Common commands:
    
    apply Builds or changes infrastructure
    
    console Interactive console for Terraform interpolations
    
    destroy Destroy Terraform-managed infrastructure
    
    env Workspace management
    
    fmt Rewrites config files to canonical format
    
    get Download and install modules for the configuration
    
    graph Create a visual graph of Terraform resources
    
    import Import existing infrastructure into Terraform
    
    init Initialize a Terraform working directory
    
    output Read an output from a state file
    
    plan Generate and show an execution plan
    
    providers Prints a tree of the providers used in the configuration
    
    push Upload this Terraform module to Atlas to run
    
    refresh Update local state file against real resources
    
    show Inspect Terraform state or plan
    
    taint Manually mark a resource for recreation
    
    untaint Manually unmark a resource as tainted
    
    validate Validates the Terraform files
    
    version Prints the Terraform version
    
    workspace Workspace management
    
      
    
    All other commands:
    
    debug Debug output management (experimental)
    
    force-unlock Manually unlock the terraform state
    
    state Advanced state management

  

- ## Common commands

- ### Apply

    Usage: terraform apply [options]  [DIR-OR-PLAN]
    
      
    
    Builds or changes infrastructure according to Terraform configuration
    
    files in DIR.
    
      
    
    By default, apply scans the current directory for the configuration
    
    and applies the changes appropriately. However, a path to another
    
    configuration or an execution plan can be provided. Execution plans can be
    
    used to only execute a pre-determined set of actions.
    
      
    
    Options:
    
      
    
    -backup=path Path to backup the existing state file before
    
    modifying. Defaults to the "-state-out" path with
    
    ".backup" extension. Set to "-" to disable backup.
    
      
    
    -auto-approve Skip interactive approval of plan before applying.
    
      
    
    -lock=true Lock the state file when locking is supported.
    
      
    
    -lock-timeout=0s Duration to retry a state lock.
    
      
    
    -input=true Ask for input for variables if not directly set.
    
      
    
    -no-color If specified, output won't contain any color.
    
      
    
    -parallelism=n Limit the number of parallel resource operations.
    
    Defaults to 10.
    
      
    
    -refresh=true Update state prior to checking for differences. This
    
    has no effect if a plan file is given to apply.
    
      
    
    -state=path Path to read and save state (unless state-out
    
    is specified). Defaults to "terraform.tfstate".
    
      
    
    -state-out=path Path to write state to that is different than
    
    "-state". This can be used to preserve the old
    
    state.
    
      
    
    -target=resource Resource to target. Operation will be limited to this
    
    resource and its dependencies. This flag can be used
    
    multiple times.
    
      
    
    -var 'foo=bar' Set a variable in the Terraform configuration. This
    
    flag can be set multiple times.
    
      
    
    -var-file=foo Set variables in the Terraform configuration from
    
    a file. If "terraform.tfvars" or any ".auto.tfvars"
    
    files are present, they will be automatically loaded.

  

- ### Destroy

    Usage: terraform destroy [options]  [DIR]
    
      
    
    Destroy Terraform-managed infrastructure.
    
      
    
    Options:
    
      
    
    -backup=path Path to backup the existing state file before
    
    modifying. Defaults to the "-state-out" path with
    
    ".backup" extension. Set to "-" to disable backup.
    
      
    
    -auto-approve Skip interactive approval before destroying.
    
      
    
    -force Deprecated: same as auto-approve.
    
      
    
    -lock=true Lock the state file when locking is supported.
    
      
    
    -lock-timeout=0s Duration to retry a state lock.
    
      
    
    -no-color If specified, output won't contain any color.
    
      
    
    -parallelism=n Limit the number of concurrent operations.
    
    Defaults to 10.
    
      
    
    -refresh=true Update state prior to checking for differences. This
    
    has no effect if a plan file is given to apply.
    
      
    
    -state=path Path to read and save state (unless state-out
    
    is specified). Defaults to "terraform.tfstate".
    
      
    
    -state-out=path Path to write state to that is different than
    
    "-state". This can be used to preserve the old
    
    state.
    
      
    
    -target=resource Resource to target. Operation will be limited to this
    
    resource and its dependencies. This flag can be used
    
    multiple times.
    
      
    
    -var 'foo=bar' Set a variable in the Terraform configuration. This
    
    flag can be set multiple times.
    
      
    
    -var-file=foo Set variables in the Terraform configuration from
    
    a file. If "terraform.tfvars" or any ".auto.tfvars"
    
    files are present, they will be automatically loaded.

  


# Terraform FAQS









