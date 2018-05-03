<!-- TITLE: Savvydownloaderscheduler -->
<!-- SUBTITLE: A quick summary of Savvydownloaderscheduler -->

# <span id="title-text">IT Procedures : SavvyDownloadScheduler</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

### Purpose

This application allows scheduling of web downloads (FTP, HTTP, etc.) at set times or frequencies.

It currently downloads around 65,000 files per month as a result of around 150 jobs scheduled through the application.

### Technical Details

This application is a SavvyPlus-developed console application written in Python.

It runs on MEL-SVR-AP-001 as a scheduled task and is designed to run continuously.

The application is located at E:\SavvyApps\SavvyDownloadScheduler\dist\SavvyDownloadScheduler and writes log files to E:\ApplicationLogs

Database connection string is set in config file SavvyDownloadScheduler.cfg

The application writes to and reads from the MarketData database. Configuration table is NEMWebFolders and file download records are stored in NEMWebFiles 

The application needs certificate file cacert.pem present in application folder to run successfully

### Monitoring and trouble-shooting

There is indirect monitoring of this application via a SQL Server Agent job that runs each hour. If no files have been loaded by the SavvyDataLoader in the last hour then an email is sent to the SQLAdmin email list. If such an email is received then the SavvyDownloadScheduler not running correctly is one possible cause.

If the application is not successfully downloading files then re-starting the application is the only thing generally required.

For more advanced trouble-shooting consult the log file or run the application from a dos box to see error messages.

### Scheduling Downloads

If a new scheduled download is added or an existing one modified then the application needs to be re-started for the changes to take effect.

Download jobs are set up using table MarketData.dbo.NEMWebFolders. Parameters are as follows:

<div class="table-wrap">

<table class="confluenceTable"><colgroup><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Parameter</th>

<th class="confluenceTh">Description</th>

</tr>

<tr>

<td class="confluenceTd">URL</td>

<td class="confluenceTd">URL from which to download. Can contain {year},{month},and/or {day} in which case the download running date will be substituted in yyyy, mm, dd format</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">interval_minutes</td>

<td colspan="1" class="confluenceTd">interval (in minutes) between downloads</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">start_time</td>

<td colspan="1" class="confluenceTd">time of day to begin the download.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">active_flag</td>

<td colspan="1" class="confluenceTd">1 makes the job active, 0 makes it inactive</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">destination_folder</td>

<td colspan="1" class="confluenceTd">folder (on relevant server) to which downloaded files should be written</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">retrieval_type</td>

<td colspan="1" class="confluenceTd">

LINKS - Use if the specified URL has links to the actual files to be downloaded. Only NEW files will be downloaded (i.e. new files names, not ones already stored in database as being downloaded previously). Only links matching _filename_pattern_ will be downloaded.

FTP_FILES - Downloads files from an FTP folder specified by _URL_. Files matching _filename_pattern_ will be downloaded. Previously downloaded file names will be ignored.

DIRECT_FTP - Downloads the file at the named _URL_ via FTP. The _URL_ should include the full file name, and _filename_pattern_ is used to determine the name of the file written at the destination.

LINKS_OVERWRITE - same as LINKS but will download all matching files irrespective of whether the same named file has previously been downloaded.

DIRECT - Downloads the file at the named _URL_ via HTTP.

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">filename_pattern</td>

<td colspan="1" class="confluenceTd">The file mask used to determine which links/files to download, or the pattern for the file name to save to (depending on _retrieval_type)_. If it contains {year} or {month} or {day} then these will be replaced with the year, month or day of the download.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">utc_offset_hours</td>

<td colspan="1" class="confluenceTd">The {year}, {month} and {day} will be the UTC time offset by this number of hours i.e. +10 will be the current AEST time, -14 will be yesterday's date in AEST.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">user_description</td>

<td colspan="1" class="confluenceTd">Description of the download job. Not used by the system</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">warning_minutes</td>

<td colspan="1" class="confluenceTd">If this particular job has not downloaded anything for longer than _warning_minutes_ then it indicates a problem with the data feed. Not used by the system.</td>

</tr>

</tbody>

</table>

</div>

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>