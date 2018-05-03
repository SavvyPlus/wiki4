<!-- TITLE: Restore A File From Backup -->
<!-- SUBTITLE: A quick summary of Restore A File From Backup -->

# <span id="title-text">IT Procedures : Restore a file from backup</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

Log in to MEL-SVR-BK-001

Start→Right click→All Apps

Open Veeam backup & Replication Console

Press "Connect"

Home→Restore

Guest files (Windows)->Next (_this specifies to restore a file from within one of the individual VMs)_

Select MEL-SVR-DC-001 (for S:\). Choose a backup copy based on the restore point

Hit Finish

A window pops up as it mounts backup. Can choose what to restore

E:\ServerFolders\CompanyData is the S: location. Select the file to restore

Click Restore→ Keep (keeps the existing copy of the file and restores a new copy?) and wait for the process to finish

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>