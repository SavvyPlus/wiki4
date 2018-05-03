<!-- TITLE: Pritunl And OpenVPN Site To Site Configuration -->
<!-- SUBTITLE: A quick summary of Pritunl And OpenVPN Site To Site Configuration -->
This guide walks through how to setup an OpenVPN client on Pfsense to connect to the Pritunl VPN server.

It is designed to create a site-to-site (ie. the OpenVPN client acts as a gateway for that network).

The network topology is as follows:

**DC1 network > Pritunl Server > Internet > pfsense (OpenVPN client) > MEL networks**

# Pritunl Setup as a Server
* On the Pritunl server, setup a new user without username/password
* Add network addresses under 'network link'
* Important: Pritunl > Server > <name> > Advanced > uncheck Restrick Routing
* Download user profile (.ovpn)
* Note for AWS Pritunl Servers, Disable Check/Source Dest

# OpenVPN Client on Pfsense
* Import CA cert and User Cert
* Add an OpenVPN client to pfsense firewall with same parameters 
* Leave username/pwd blank
* Use TLS cert from .ovpn profile
* Use Compression with Adaptive setting
* Note: The OVPN client pulls other routes from server, just add one, it will pull the remaining (check Routes on firewall)
* Create firewall rules on OpenVPN interface (use packet capture to find source/dest IPs)
* On the firewall rules, select Advanced and set the Gateway to the interface of the Openvpn interface (if it doesn't exist, go to Interfaces > Assign, assign the new OpenVPN interface a name and create it)
* Then go to NAT > Outbound, create a NAT rule
* Select Interface as the OpenVPN interface
* Set Source as the local subnets (10.61.1.0/24 for example) (best to create an alias here)
* Set Destination as the destination subnets (best to create an alias here)
* Leave all other settings, click Save