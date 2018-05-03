<!-- TITLE: Getting Started -->
<!-- SUBTITLE: A quick summary of how to get going in this complicated world -->

# The basics
So to begin with, we are Savvy, a bunch of people looking to use tech to change the world.  Ok that could be an overstatement, but we are passionate about tech and want to develop tools to improve business processes, model data and develop cool stuff.

Now you're part of the Savvy team, you'll need a few things to get going.  We host most of our infrastructure in AWS.  Don't know what AWS is, you probably shouldn't be working with us hehe.

To get connected to our network which we've built from the ground up, you'll either be granted one of these two options;
**- Option A - VPN connectivity using your own computer**
**- Option B - AWS Workspace with a virtual hosted desktop**

Either way you'll be given a Windows credentials where most services and apps authenticate against.

**When you join Savvy, you'll be given...**
* Windows Username and Password
* Either a VPN profile (Option A) or AWS registration code for your Workspace (Option B)

Follow the section below depending on what you've been allocated to, then keep reading.

# Option A - VPN connectivity
Here at SavvyBI, we have provisioned a VPN server (Pritunl – www.pritunl.com) which is configured to allow our development team to connect to our network.

1.	Download the Pritunl VPN client:
							Windows: https://client.pritunl.com/#install
							Mac:  https://client.pritunl.com/#install
							Other: https://client.pritunl.com/#install
2.	Follow the prompts to install the VPN client
3.  Open Pritunl, and select ‘Import Profile’.  Import the .TAR profile sent to you.
4.  Once imported, select the connection and click 'Connect'
5.  Enter your Windows password when prompted
6.  You are now connected to the network

# Option B - AWS Workspace
Here at SavvyBI, we have provisioned a virtual desktop with all the apps you need running Windows 10 which is hosted with Amazon Web Services (AWS) Workspaces.  You have your own virtual desktop along with a User drive to store temporary data.  A standard set of apps have already been deployed for your convenience.  Your virtual desktop is available 24x7 and you can connect anywhere you like using a web browser or client.
Your virtual desktop is configured with Active Directory authentication to the Savvy domain, which will gain you access to the resources you need.  No VPN access is required as your virtual desktop is hosted within the AWS infrastructure.

1.	Browse to: https://clients.amazonworkspaces.com/
2.	Download the client for your OS
3.	Launch app once installed and enter your registration code provided to you
4.	Enter your provided Windows Username and Password to connect

# Accessing the Infrastructure
Once you are connected we have a webapp called Guacamole which is a single portal for server access.
Guacamole is configured for the appropriate protocol (eg. SSH, RDP) and port to connect to the server.
All servers are configured with Active Directory authentication so use your Windows credentials to login.

1.	Browse to https://access.savvy.work
2.	Login with your Windows username and password
3.	Once logged in, click on a server to connect to
4.	Login with your Windows username and password 

# Frequently Asked Questions
**Q. Where do I store common documents/data?**
A.  You will have granted access to Google Drive, launch the Google Stream app on your virtual desktop and login with your personal email address

**Q. What are the standard apps we should use?**
A. 
•	Sublime – code writing, txt editing
•	Github Desktop – code management
•	Slack – chat communication
•	Asana – project and task management
•	SQL Management Studio – SQL access
•	Guacamole – server access (see question below)
•	Chrome – web browsing
•	7-zip – compression tool
•	CoreFTP – FTP client
•	Java – JRE
•	Putty – direct SSH/telnet access

**Q. What are the communication channels?**
A. 
Slack – for chat communication.  Join a slack channel related to your work.
Asana – for project management
Email – last resort

**Q. I’m looking for help, who do I ask?**
A. 
@elpresi – for general guidance
@jamesdaley – for infrastructure/connectivity
@jarrod - BI reporting



