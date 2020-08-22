---
layout: post
title: Don't use ec2 before you read this
date: 2020-07-22 13:32:20 +0300
description: Planning to use EC2? read this first # Add Post Description (Optional)
img: icons/electronics.svg #I-Rest.Jpg # Add Image Post (Optional)
fig-Caption: Image # Add Figcaption (Optional)
tags: [aws,ec2,instance,elastic compute cloud]
---


## What is EC2? 

Ever since we moved into a new IT century, computing has become more and more important.

For organizations big and small, it is important to have reliable and highly available computing resources. Companies use these resources to provide support for their critical business operations. 

Companies have to set up their infrastructure to access computing power. They have to spend a lot of money hiring people, setting up servers, buying data centers, and infrastructure to be reliable and scalable.

Amazon's elastic computer cloud or commonly known as  ec2 is a service that provides all the above features without having to worry about the infrastructure.  Since EC2 service is based on the model that you only pay for the resources you use,  it's a great way to get all the computing power without spending a lot of money on the infrastructure.  


## Why Use EC2? 

EC2 service is also very scalable. What I mean by that is companies can increase or decrease the resource uses and resource availability depending on their requirements. If you are a small firm and cannot afford to spend a lot of money on server infrastructure, you can spin up an EC2 instance and serve your users. 

If you are famous and need more computing power, you can spin up new EC2 boxes or you can increase the capacity of the existing EC2 boxes to meet your new popularity.  


## How EC2 works? 

First, EC2 service is essentially a virtual environment that lives in the cloud. Such an environment is called an instance. To create these instances, you need to supply the details such as what type of operating system you would like or what type of software should be installed when setting up this instance. These configuration templates are called AMI. 

Further, these instances are grouped according to different system parameters. You can have combinations based on  CPU, Ram, or storage. When you combine these instances based on the above system parameters, these are called instance types.


### Storage options in EC2? 


It is important to note the different options EC2 service provides for storage. You can have two types of storage for any EC2 box.  The first type of storage is temporary storage that comes by default with any EC2 instance. This storage is ephemeral as in if you store files or data in this storage, and you stop or restart your instance, you will lose all the data or the files. We should not use this storage for persistent files or data. 


When you need more durable storage, you can use EBS. EBS is persistent storage and will hold your data or files even if the EC2 instance is shutdown or restarted.


### How do you login to the EC2 instance? {#how-do-you-login-to-the-ec2-instance}


You might wonder how you can log in to such a virtual server?


When you create an instance, AWS also creates two pairs of keys for this instance. These keys are the public and private keys of the instance. These two keys are essential to log in and perform operations in the instance. 


When you create an instance, you can download a private key and a public key will live on the EC2 instance. You can then log into the EC2 box using the combination of the public and private keys. This ensures that only the person who has the private key can log in to the Box.


To secure any EC2 instance, AWS provides a firewall. Firewalls can help protect your EC2 instance by limiting the port, protocol, or the IP address that can access your box.


EC2 service also provides a way to publicly access your instance. It assigns an IP address for each instance, which is called an elastic IP.


### How do you organize instances? {#how-do-you-organize-instances}


When you have too many of these EC2 instances, sometimes it can become hard to organize them. To overcome this problem, you can use EC2 tags.  Tags provide a neat way to organize all of your instances. You can assign tags based on the instance name, Department name, or even the functional use of the instance.


Ideally, you should group all of your related resources inside a VPC for security.


Now that I have told you a little about EC2 service, I will tell you some of the best practices you can use to get the maximum value out of the EC2 service.


## Tips for EC2? {#tips-for-ec2}



1. EC2 instances cost you money so if you're not using them either stop them or even better, terminate them.
2. Whenever you want to use any EC2 instance, make sure that you fully understand the requirement of your application.  The reason for this is that if you know your requirements (for example, how much CPU you need, how much storage you need), you can select the EC2 instance type that suits your requirement perfectly.
3. EC2 service also provides auto-scaling, and this can be used in situations when you are expecting increased traffic or load to your application.
4. If the above does not work for you, then you can also look into the load balancer. A load balancer allows you to seamlessly integrate different EC2 instances to provide maximum reliability for your application.
5.  It is important not to have a single point of failure in your application. You can do that by dividing your application into smaller components. These smaller components can then be hosted in suitable EC2 instances. To further increase the reliability and fault tolerance of your system, you can think about distributing these instances between different availability zones.
6. A great way to reduce your EC2 service cost is to go for reserved instances. These are the instances where you need to reserve an EC2 instance for a longer period. By reserving the EC2 service for a longer duration of time, you can reduce the cost up to 60 to 70%
7. Never disclose your private key to unauthorized users.  Never leave these Keys either in your Source control or inside an EC2 instance. If you lose your private key, you cannot log in to your EC2 instance, so keeping it safe should be very important.
8. If you need to persist your data, do not store it in the EC2 default storage. Always go for EBS, which is durable.
9. Use tagging to organize your resources so you and your team members can easily find the resource you are looking for.


## Where can I learn more? {#where-can-i-learn-more}

In this article, I gave you a brief introduction to EC2 service and when to use it. I also gave you a few tips to use it more efficiently.  

I hope you like this article.

I would talk about other interesting features of EC2 service in upcoming articles.

Thank you
