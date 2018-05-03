<!-- TITLE: Failing Over PFsense From Production To Failover Devices -->
<!-- SUBTITLE: A quick summary of Failing Over PFsense From Production To Failover Devices -->


1. Connect to backup-pfsense on port igb0 (LAN_mgmt)
1. Browse to https://192.168.100.254:40443
1. Login with username: james.daley and password: <usual>
1. Confirm the backup-pfsense is running the same version as the production-pfsense firewall
1. Go to Diagnostics > Backup & Restore
1. Browse to most recent version, select Restore Configuration
1. An interface mismatch will be detected, to correct this:
* WAN - igb1
* LAN_mgmt - igb0
* OPT1 - igb2
* OPT2 - igb2
* OPT3 - igb2
* OPT4 - igb2
8. Click Save
9. Then go to tab VLANS, then assign all vlans to igb2 (OPT1) - this will be slow
10. Unplug the network patch leads from the production-pfsense
11. Plug in the network patch leads (WAN, vlan_trunk)
12. Should be good-to-go