<!-- TITLE: Creating An EC2 Instance -->
<!-- SUBTITLE: A quick summary of Creating An Ec 2 Instance -->

# Creating an EC2 instance.  Which network settings do I choose?
This is a quick tutorial on how to create an EC2 instance in AWS.  This illustrates the selecting the appropriate network settings for an instance.

Now for this example we are going to create an Ubuntu t2.micro instance which is for a Development project which will be located in AWS Sydney (AWS2).

### 1. Login to the **AWS console** at: https://aws.amazon.com/console/

### 2. Select **Services** > **EC2** so you arrive here.

![1](/uploads/1.png "1")

### 3. Select **Launch Instance**

### 4. Select **Ubuntu Server 16.04 LTS (HVM), SSD Volume Type**'

![2](/uploads/2.png "2")

### 5. Select the instance type, here we choose **t2.micro** and select **Next: Configure Instance Details**

![3](/uploads/3.png "3")

### 6. On the next page we need to select the network config.  Here we are assuming this instance is for a Development project.  Therefore, select:
#### VPC: aws2_vpc_dts (this is the dev/test/staging VPC)
#### Subnet: aws2_sub_dev_priv_2a (this is the Development subnet, which is also Private (it will only be accessed internally) and is located in the 2a Availability Zone).

![4](/uploads/4.png "4")

### 7. Select **Next: Add Storage**

### 8. Select the size and type of disk(s) you require.  In this example, we'll leave the default of **8GB** and **General Purpose SSD**

![5](/uploads/5.png "5")

### 9.  Select **Next: Add Tags**

### 10. There is no need to add tags in this example, select **Next: Configure Security Group**

### 11.  We want to specify an existing Security Group.  Do not choose Create a new Security Group.  
### Choose **Select an existing security group**

### 12.  For this example we want to choose the Security Group which aligns to the Subnet.
### Choose **aws2_sg_dev_priv** (this aligns with subnet aws2_sub_dev_priv_2a)



13.  



