<!-- TITLE: Windows 10 Deployment Procedure -->
<!-- SUBTITLE: A quick summary of Windows 10 Deployment Procedure -->

# Existing Computers
1. Remove computer object from Active Directory and force replicated changes
1. Remove Webroot agent from console
1. When joining the computer to the domain, add as a new name (PDQ issues otherwise)
# New Computers
1. Boot into BIOS > Change disk type to SATA from AHCI to IDE
1. Boot from USB drive (F12)
1. Installer will complete W10 installation
1. Once complete, run the Powershell script on desktop to join to domain
1. Check drives installed correctly and are complete, otherwise use Windows Updates to search and automatically install drivers
1. Login to a domain controller and confirm computer object is present.  If not, force AD replication and reboot SOE computer.  It often takes a few minutes to appear.
1. Login with the local Administrator account and check drivers are installed, LEAVE account logged-in whilst deploying via PDQ
1. Deploy PDQ schedules; A (add new computer to this schedule), B (automatic), C (add computer to schedule)
1. Test login with account SAVVYPLUS\SOE (usual Savvy pwd)
1. Email default template to user
1. Log into AD and add user as description on computer object
1. Label with printed tag