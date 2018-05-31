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

## 

### Naming Conventions

So here we use a standard naming convention which helps understanding what goes where.  

It usually goes something like this, here's some examples.

aws2_vpc_mgmt - this is AWS2 which is Sydney, VPC, and the Management VPC

aws2_sub_dev_priv_2a - this is AWS2 which is Sydney, Sub which is a subnet, Dev which is Development, Priv which is a Private subnet (behind NAT) and 2a which is the Availability Zone.

aws2_sg_prod_pub - this is AWS2 which is the Sydney site, SG which is a Security Group, Prod which is the Production subnet, Pub which is a Public subnet (has its own dedicated Public IP address).