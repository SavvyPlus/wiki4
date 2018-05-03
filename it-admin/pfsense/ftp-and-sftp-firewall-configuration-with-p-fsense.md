<!-- TITLE: FTP / SFTP Firewall Configuration With PFsense -->
<!-- SUBTITLE: A quick summary of FTP And SFTP Firewall Configuration With PFsense -->

# FTP Configuration
## Pfsense:
* NAT ports tcp\21, tcp\20, tcp\<passive port range of ftp server>
* Create associated firewall rules for this
* Whitelist WAN ip addresses from clients you trust and add them in the NAT rule (it will update the firewall rule)
## Syncplify FTP:
* Under Syncplify Server > Securrity > FTP
* Check the PASV port range and allow 100 ports of so, then NAT these to the server in Pfsense
* Set the WAN IP address in the field 
* External IP for PASV connections
# SFTP Configuration
## Pfsense:
NAT ports tcp\22
Create associated firewall rules for this
Whitelist WAN ip addresses from clients you trust and add them in the NAT rule (it will update the firewall rule)