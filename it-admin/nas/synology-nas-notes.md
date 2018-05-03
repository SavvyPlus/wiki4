<!-- TITLE: Synology NAS Notes -->
<!-- SUBTITLE: A quick summary of Synology NAS Notes -->

# Having issues connecting via SMB?
* Try connecting to the IP address of the NAS, not the hostname
* Restart the SMB service on the NAS (Control Panel > Info > Services > uncheck/recheck service)
* Confirm network settings including DNS
* Refresh Domain Directory (to reimport all domain user accounts)
* Use a simple password for domain authentication (no special characters)
* On the Windows server, check the Credential Manager for cached passwords
* Reset the backup.admin password