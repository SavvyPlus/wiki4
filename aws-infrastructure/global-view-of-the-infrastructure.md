<!-- TITLE: Global View Of The Infrastructure -->
<!-- SUBTITLE: A quick summary of Global View Of The Infrastructure -->

# Global View of the Infrastructure

## Quick intro
We use Amazon Web Services to host all of our infrastructure for SavvyBI and about half of SavvyPlus (the rest of SavvyPlus is hosted internally in the Melbourne Office).

This intro will talk through the services and network side of our infrastructure, which is really important to understand.  Why?  Well you'll spin a new EC2 instance and you wont be able to connect. Why? Well read on to understand why.

## AWS Lingo
So, AWS hey.  To begin with you need a basic understanding of the terminology before we get started.  

In AWS, they use they're own terminology which is useful to understand.

* **VPC** - Virtual Private Cloud.  This is the whole network which subnets exist within.  Think of it like a big container or group of little networks.
* **Subnets** - Subnets are well... Sub-networks.  These define where network objects sit (ie. servers etc).  They are either Private (which sit behind a NAT and don't have their own external IP address) or Public (have their dedicated public IP address).  When to use what? Well use Private unless it should be publically facing (such as a web server), otherwise put it in a Public subnet.
* **Availability Zones** - these are like little datacentres, so for services which require high availablity, we duplicate them across more than one AZ for redundancy.  
* **Security Groups** - these are groups of firewall ports which allow traffic in/out of subnets.  Think of them as our firewall.

The diagram below shows all the components.

![Internet Gateway Diagram](/uploads/internet-gateway-diagram.png "Internet Gateway Diagram")

More here: https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html

## AWS Regions we use
We use different AWS regions (locations) for different services though most are hosted in AWS2.

* AWS1 - Ohio 
* AWS2 - Sydney (most things live here)
* AWS3 - Singapore
* AWS4 - Oregon
* AWS5 - Tokyo

## Our VPCs
Across all sites we use standard naming for our VPCs.  These include (where awsx represents the region)...
* awsX_vpc_mgmt - this is the Management VPC for the servers that look after authentication, app deployment, backups etc
* awsX_vpc_prod - this is the Production VPC for the production services.  
* awsX_vpc_dts - this is the Development/Testing/Staging VPC.  For all our dev team, most of your work will sit in here.
* awsX_vpc_vdi - this is the Virtual Desktop Infrastructure (known as AWS Workspace) for our virtual desktops.

## Which Subnets for what?
Each VPC is broken down into smaller sub-networks (aka subnets!).  As mentioned previously each subnet is either Private or Public.
A quick reminder...
* Private - used for most services, they sit behind a NAT and are only accessible internally.  This is the most secure option and where our services should sit by default.  If you're not sure, put it in here.
* Public - used only for services which need a Public IP address.  Only for web servers really that need public access.  Don't put things in this subnet because you're not sure.

Then for the Availability Zones (AZs).  Well for all Dev/Test/Staging just pick the lowest AZ (ie. 2a or 1a).  For Production and Management, @elpresi and @jamesdaley can assist with this setup (its app specific).

And finally, not every subnet has a public subnet btw.  Some just don't need them (for example Dev and Test should remain in-house so shouldn't need a Public subnet).

## Security Groups
Security groups have been setup so they correlate to subnets.  This ensures the basic connectivity will work.  

For example, if you are using the subnet below... 
aws2_sub_dev_priv_2a

Then assign security group...
aws2_sg_dev_priv

On top of that we can assign what we call "app" security groups for specific services.  
These are specific purposes to allow traffic into public IP addresses.  These are defined with logical names as per above, though if unsure, contact @jamesdaley.
Note: These are only necessary for Public subnets.

## Naming Conventions

We use a standard naming convention which helps understanding what goes where.  

It usually goes something like this, here's some examples.

aws2_vpc_mgmt - this is AWS2 which is Sydney, VPC, and the Management VPC

aws2_sub_dev_priv_2a - this is AWS2 which is Sydney, Sub which is a subnet, Dev which is Development, Priv which is a Private subnet (behind NAT) and 2a which is the Availability Zone.

aws2_sg_prod_pub - this is AWS2 which is the Sydney site, SG which is a Security Group, Prod which is the Production subnet, Pub which is a Public subnet (has its own dedicated Public IP address).