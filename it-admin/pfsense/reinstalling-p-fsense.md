<!-- TITLE: Reinstalling PFsense -->
<!-- SUBTITLE: A quick summary of Reinstalling PFsense -->

# Reinstalling PFsense on a Netgate SG-8860 1U Firewall
### Current Config on Pfsense SG-8860 1RU:

**Interface Networks:**

WAN - Internet - 103.249.67.142/32 (Static IP with Gateway configured)
LAN - Management (no VLAN) - 192.168.100.254/24 (DHCP disabled)
OPT1 - mel_vlan_svrs - 10.61.1.254/24 (VLAN 101)
OPT2 - mel_vlan_clts - 10.61.3.254/24 (VLAN 103)
OPT3 - mel_vlan_wifi_trust - 10.61.6.254/24 (VLAN 106)
OPT4 - mel_vlan_wifi_guest - 10.61.7.254/24 (VLAN 107)

**Web Interface Access:**

* https://10.61.3.254:40443/ (from vlan 103)
* https://103.249.67.142:40443/ (from WAN - only James Daley No-IP address_
* https://192.168.100.254:40443 (from LAN port)

***Things to note:***

Hardware you will need:

* USB stick
* USB mini to USB cable
* Ethernet Cable

Software you will need:

* Pfsense backup (and version no.) 
* 7zip portable https://portableapps.com/apps/utilities/7-zip_portable
* Rufus (USB boot writer) https://rufus.akeo.ie/
* Putty https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html 
* C2104 USB to serial driver (Connect to the USB port, then use Windows Updates to download driver or download from link here) http://www.silabs.com/products/mcu/Pages/USBtoUARTBridgeVCPDrivers.aspx
___________________________________________________________________________________

# Recovery Procedure

## Preparation
1. Check the Dropbox DR folder for latest PFsense image and backup, else download by...
* Login to https://portal.pfsense.org/firmware/memstick/
* **Username**: savvyplus
* **Password**: 8gf3jULadZmqGi2KMbwbXeTWVC96
* **Encryption** Password: savvyplus
1. Download the NETGATE ADI x64 image (the version must correlate to the backup)
**pfSense-netgate-memstick-ADI-X.X.X-RELEASE-amd64.img.gz**
1. Download backup config (it must correlate to the version above)
1. Unzip the image using 7zip
1. Write image to USB using Rufus (fat32, default allocation)

## Connecting
1. Plugin USB cable to firewall
1. Check Device Manager and update driver using windows update
1. Change baud rate to 115200
1. Note the COM port
1. Open Putty, enter COM and baud rate as 115200
1. Insert USB stick in the TOP USB port of the firewall

## Recovery
1. Push the RED button on the back of the pfsense unit to soft power off. 
1. Once off, push again to turn on
1. The boot sequence will auto boot off the USB 
1. When prompted, select Quick/Easy installer 
1. When prompted select the model (Sg-8860-1U) - check the bottom sticker on the pfsense unit to confirm
1. Once the installer has finished, wait until you see 'Uptime' then remove the USB stick 
1. When installed, connect the Ethernet to the LAN port (LAN Management interface)
1. Set static IP on laptop to: IP: 192.168.1.200, Subnet: /24, GW: 192.168.1.1
1. Browse to web interface https://192.168.1.1 , login with username: admin ; pfsense
1. Go to Diagnostics > Backup and Restore (browse to backup config)
1. Once restore complete, set static IP on laptop to: IP: 192.168.100.200, Subnet: /24, GW: 192.168.100.254
1. Browse to https://192.168.100.254:40443 
1. Once up and running (and has internet connectivity), you can use the AutoConfigBackup to restore to the latest changes (MUST be the same version the unit is running, otherwise update it first, then restore)

#### Other notes
- sometimes it's worth rebooting the core switch