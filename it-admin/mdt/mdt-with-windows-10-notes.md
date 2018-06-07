<!-- TITLE: MDT With Windows 10 Notes -->
<!-- SUBTITLE: A quick summary of MDT With Windows 10 Notes -->

# Working functions:
RDP enabled
Start menu, remove all app icons and sets a default
Automated install with autologon 3 times
Remove all W10 apps post Windows update except important apps - Win Store, Calc etc
Onedrive still there although no prompts
Disabled Windows Defender via GPO
Disabled OneDrive via GPO
Disables Windows firewall (service remains started, it disables all the firewall profiles)
Renames system drive to 'SYSTEM'
Added a MAK product key into the Unattend XML (Specialise pass, OOBE) - there is no longer a prompt for product key!
Printers are working well - followed this guide  https://community.spiceworks.com/how_to/77664-so-you-need-to-deploy-printers-with-group-policy-windows-2012-r2
Runs a powershell function to set-execution policy to RemoteSigned for all users
Copies a powershell to the Administrators\Desktop which automatically runs with administrative credentials (UAC), prompts for the domain to join, new computer name and then performs both tasks and reboots.

# When updating the MDT ClientDeploymentShare image (captured image ready for client deployment):

Change ProtectMyPC to 3
Change Autologon (administrator) to 3 times
Delete all Specialised entries (approx 8 entries)
Add Display settings as 1,1,60,32
Add Windows 10 Product Key by:
Edit Unattend.xml (via Deployment Workbench)
Add x86 Microsoft-Windows-Shell-Setup_neutral to Pass 4 (specialise)
Remove all sub-entries except for the Product key entry
Add the Product key for Windows 10
Also add the Product key to the Rules (task sequence)
Save and exit

# Writing the MDT boot image to a USB
![Rufus](/uploads/rufus.png "Rufus")

Then in the BIOS, got to Startup > select Legacy First
Disable Secuirty > SecureBoot
Boot and wait at the Lenovo screen, it takes approx 30 seconds before booting to the MDT image
Thats it.