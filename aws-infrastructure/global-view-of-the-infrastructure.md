---
title: Global View Of The Infrastructure
description: A quick summary of Global View Of The Infrastructure
published: true
date: 2019-11-20T04:55:47.104Z
tags: 
---

# Global View of the Infrastructure

## Quick intro
We use Amazon Web Services to host all of our infrastructure for all the companies.

This intro will talk through the services and network side of our infrastructure, which is really important to understand.  Why?  Well you'll spin a new EC2 instance and you wont be able to connect. Why? Well read on to understand why.

## The networking side 

### Lingo
So, AWS hey.  To begin with you need a basic understanding of the terminology before we get started.  

In AWS, they use they're own terminology which is useful to understand.

* **VPC** - Virtual Private Cloud.  This is the whole network which subnets exist within.  Think of it like a big container or group of little networks.
* **Subnets** - Subnets are well... Sub-networks.  These define where network objects sit (ie. servers etc).  They are either Private (which sit behind a NAT and don't have their own external IP address) or Public (have their dedicated public IP address).  When to use what? Well use Private unless it should be publically facing (such as a web server), otherwise put it in a Public subnet.
* **Availability Zones** - these are like little datacentres, so for services which require high availablity, we duplicate them across more than one AZ for redundancy.  
* **Security Groups** - these are groups of firewall ports which allow traffic in/out of subnets.  Think of them as our firewall.

The diagram below shows all the components.

![Internet Gateway Diagram](/uploads/internet-gateway-diagram.png "Internet Gateway Diagram")

More here: https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html

### AWS Regions we use
We use AWS Sydney predominently, and AWS Oregon for those service which are not yet available to Sydney.


### Our VPCs
Across all sites we use standard naming for our VPCs.  These include (where awsx represents the region)... Each company has its own VPC and some have more than one.  Some can communicate with eachother but this is often changing.

### Which Subnets for what?
Each VPC is broken down into smaller sub-networks (aka subnets!).  As mentioned previously each subnet is either Private or Public.
A quick reminder...
* **Private** - used for most services, they sit behind a NAT and are only accessible internally.  This is the most secure option and where our services should sit by default.  If you're not sure, put it in here.
* **Public** - used only for services which need a Public IP address.  Only for web servers really that need public access.  Don't put things in this subnet because you're not sure.

**Availability Zones (AZs)**.  Well for all Dev/Test/Staging just pick the lowest AZ (ie. 2a or 1a).  For Production and Management, @oski and @james can assist with this setup (its app specific).

And finally, not every subnet has a public subnet btw.  Some just don't need them (for example Dev and Test should remain in-house so shouldn't need a Public subnet).

### Security Groups
Security groups are groups of ports which acts as our firewall.  When creating an EC2 instance or other object in AWS, you need to assign a security group.

For example, this one allows internal access from your computer.
aws2_sg_xxxx__int.clientaccess

This one enables other servers to communicate with eachother.
aws2_sg_xxxx__int.servercomms

You may notice these are defined by the VPC and whether its "int" (internal) or "ext" (external).  External security groups should rarely be used other than for public facing services.

### Naming Conventions

We use a standard naming convention which helps understanding what goes where.  

It usually goes something like this...

- AWS region (eg. aws2)
- Service (eg. sub) - meaning subnet
- VPC (eg. sims) - this is the Empower AWS account
- then something specific like "int" or "ext" followed by a descriptive

Please follow all existing conventions as you see them.