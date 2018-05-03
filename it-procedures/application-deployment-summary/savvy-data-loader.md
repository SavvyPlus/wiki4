<!-- TITLE: Savvy Data Loader -->
<!-- SUBTITLE: A quick summary of Savvy Data Loader -->

# <span id="title-text">IT Procedures : SavvyDataLoader</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

### Purpose

The SavvyDataLoader application is a tool to process data files and load relevant data into a database. The application comes with generic handlers to accommodate standard formats (CSV etc.) but is structured to allow the addition of other handlers for non-standard file types. It can be used to move and/or unzip zipped files for loading.

It is currently used for market data, but can also accommodate other types (e.g. by creating a 2nd instance pointing to a different database). Around 50 jobs are handled by the application as at May 2017.

### Technical Details

This application is a SavvyPlus-developed console application written in Python.

It runs on MEL-SVR-AP-001 and is started by a scheduled task. It is designed to run continuously.

The application is located at E:\SavvyApps\SavvyDataLoader\SavvyDataLoader.exe and writes log files to E:\ApplicationLogs

The application writes to and reads from the MarketData database. Configuration table is SavvyLoaderJobs and file processing records are stored in SavvyLoaderFiles

### Operation

On opening, the application reads a list of loading jobs from table SavvyLoaderJobs. Each job specifies a source folder, a handler and various parameters to pass to it, an error folder for failed files and archive folder for successfully processed files. It also specifies a retention time for successfully processed files.

During operation the application continually cycles through the following steps:

1.  Refreshes the jobs list if it has been longer than the specified time interval (e.g. 60seconds) since last done
2.  Performs a directory listing for each source folder if it has been longer than the specified time (e.g. 5 seconds) since last done, and identifies files matching each job's file name mask
3.  Determines the priority order for processing files based on each job's priority rank
4.  Processes the highest-priority file in the queue  

    1.  passes the file name/location to the specified handler
    2.  if handler returns successfully, move file to archive folder
    3.  if handler returns and error, move file to error folder
    4.  write result to SavvyLoaderFiles table
5.  Purge archive files according to each job's file mask and retention time setting

### Monitoring and Troubleshooting

This application is monitored via a SQL Server Agent job that runs each hour. If no files have been loaded by the SavvyDataLoader in the last hour then an email is sent to the SQLAdmin email list. If such an email is received then either the SavvyDataLoader or SavvyDownloadScheduler is not running correctly.

In normal operation the application is highly reliable and re-start is not required.

For advanced trouble-shooting consult the log file, or run the application from a dos box to see error messages produced.

### Application Configuration

The following parameters can be set in the config file SavvyDataLoader.cfg located in the deployment folder:

Database Connection

*   odbcconnectionstring: ODBC database connection string to connect to database
*   retry_time_seconds: time (seconds) to wait between database connection re-tries (e.g. 5)

Refresh Times

*   source_locations_refresh_seconds:  time interval (seconds) between refreshing the list of source locations to load files from (e.g. 60)

*   source_files_refresh_seconds: time interval (seconds) between polling the source folders to look for new files (e.g. 5)

*   archive_purge_delay_minutes: time interval (minutes) at which to purge archive folders (e.g. 1)

### Configuring Data Loading Jobs

Jobs are managed through the SavvyLoaderJobs table. The fields are as follows:

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Field</th>

<th class="confluenceTh">Purpose</th>

</tr>

<tr>

<td colspan="1" class="confluenceTd">source_folder</td>

<td colspan="1" class="confluenceTd">The folder to watch for files to process. This should be a local folder on the server running the application as reliable access is assumed.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">success_folder</td>

<td colspan="1" class="confluenceTd">The folder in which to place files after successful processing. This is also the location against which the file purging process will operate.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">fail_folder</td>

<td colspan="1" class="confluenceTd">The folder in which to place files that are not successfully processed.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">priority</td>

<td colspan="1" class="confluenceTd">The job priority. Jobs with lower numbers will be processed before those with higher numbers</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">active_flag</td>

<td colspan="1" class="confluenceTd">1 = active, 0 = inactive. Use to temporarily disable jobs without deleting configuration</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">filename_pattern</td>

<td colspan="1" class="confluenceTd">dos-style file name matching string e.g. *.zip</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">handler</td>

<td colspan="1" class="confluenceTd">text matching an entry in the table of handlers below</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">handler_params</td>

<td colspan="1" class="confluenceTd">Text that evaluates to a Python dict containing parameters to pass to the handler. Description/examples below</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">success_retention_days</td>

<td colspan="1" class="confluenceTd">

Number of days to retain archived files. Files in archive older than this date will be purged.

-1 indicates keep files forever

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">job_description</td>

<td colspan="1" class="confluenceTd">User description of the job. Not used by the system</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">warning_minutes</td>

<td colspan="1" class="confluenceTd">If the job has not processed a file for this many minutes it may indicate a problem with the data feed.</td>

</tr>

</tbody>

</table>

</div>

######   Existing Handlers

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Handler</th>

<th colspan="1" class="confluenceTh">Type</th>

<th class="confluenceTh">Role</th>

</tr>

<tr>

<td class="confluenceTd">csv_handler</td>

<td colspan="1" class="confluenceTd">Generic</td>

<td class="confluenceTd">Highly configurable handler to load any CSV file into a specified database location. See detail below.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">move_only</td>

<td colspan="1" class="confluenceTd">Generic</td>

<td colspan="1" class="confluenceTd">Returns successfully without loading any data. File is moved from source to archive folder.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">unzip</td>

<td colspan="1" class="confluenceTd">Generic</td>

<td colspan="1" class="confluenceTd">Unzips the file in-place i.e. extracts the zipped file to the same location</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">asx_handler</td>

<td colspan="1" class="confluenceTd">Specific</td>

<td colspan="1" class="confluenceTd">Load various ASX files (settlement, end of day snapshots, open interest files) into the appropriate MarketData tables</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">tasHydro_handler</td>

<td colspan="1" class="confluenceTd">Specific</td>

<td colspan="1" class="confluenceTd">Load Hydro Tasmania weekly rate card files into the appropriate MarketData table</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">precis_forecast_handler</td>

<td colspan="1" class="confluenceTd">Specific</td>

<td colspan="1" class="confluenceTd">Load Bureau of Meteorology precis forecast files into the appropriate MarketData table</td>

</tr>

</tbody>

</table>

</div>

###### CSV Handler

The CSV handler is the most useful and generic handler available and can be used to process a large number of CSV files and variants. The following parameters are available as part of the CSV handler.

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Parameter Name</th>

<th class="confluenceTh">Usage</th>

</tr>

<tr>

<td colspan="1" class="confluenceTd">dest_table</td>

<td colspan="1" class="confluenceTd">Required parameter. This specifies the name of the table into which data will be loaded.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">header_end_text</td>

<td colspan="1" class="confluenceTd">Text that marks the end of the header text to be stripped away leaving data in CSV form. Useful when number of lines of header text is unknown but the header ends in a known character sequence. Optional parameter</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">footer_start_text</td>

<td colspan="1" class="confluenceTd">Text that marks the start of the footer text to be stripped away leaving data in CSV form. Useful when number of lines of footer text is unknown but the footer starts with a known character sequence. Optional parameter</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">key_fields</td>

<td colspan="1" class="confluenceTd">List or set of field names that represent a natural key for the particular data set being loaded. New data loaded with the same combination of values for each key_field will result in an update to the existing record. New combinations of values for each key_field will result in an insert. A single file should not contain multiple rows with an identical combination of values for the key_fields. If key_fields is None then each new record found will be inserted.</td>

</tr>

</tbody>

</table>

</div>

In addition to the parameters above you can also use any of the arguments accepted by the pandas library's read_csv function. Documentation is at [http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)

Examples:

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">handler_params value</th>

<th class="confluenceTh">Meaning</th>

</tr>

<tr>

<td colspan="1" class="confluenceTd"> {'dest_table':'ASX_Tradelog', 'skiprows':1, 'parse_dates':[0], 'dayfirst':True, 'key_fields':[]}</td>

<td colspan="1" class="confluenceTd">Destination table to write to is ASX_tradelog. Skip 1 header row at start of file. Interpret column 0 (first column) as a date, and interpret dates assuming dd/mm rather than mm/dd format. No key_fields therefore insert every record and never update an existing record</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd"> {dest_table':'AEMO_NSLP', 'header_end_text':r'', 'footer_start_text':r'', 'parse_dates':[2,3], 'dayfirst' : True, 'key_fields' : ['profilename','profilearea','settlementdate']}  </td>

<td colspan="1" class="confluenceTd">Destination table is AEMO_NSLP. Ignore header and footer, dealing only with text between and  Cols 2 and 3 are dates in a day/month format. A natural key for the data is profilename, profilearea and settlementdate.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">{'dest_table':'AEMO_CDEII','key_fields':['settlementdate','regionid'],
'skiprows':1,'skipfooter':1,'usecols'
['CONTRACTYEAR','WEEKNO','SETTLEMENTDATE','
REGIONID','TOTAL_SENT_OUT_ENERGY','TOTAL_EMISSIONS','CO2E_INTENSITY_INDEX']}</td>

<td colspan="1" class="confluenceTd">Write to table AEMO_CDEII, which will have unique records by settlementdate and regionid. Skip 1 header row and 1 footer row. Use a named subset of the columns only.</td>

</tr>

</tbody>

</table>

</div>

The CSV handler uses a function to clean field names and ensure they are valid and suitable for the database. Cleaning steps are:

1.  Leading & trailing whitespace is removed
2.  If a number in square brackets appears on the RHS of the string it is removed
3.  Any character that's not alphanumeric or underscore is replaced with underscore
4.  Leading & trailing underscores are removed
5.  If the 1st character is numeric underscore is prepended
6.  Characters are converted to lower case

### Compiling

The application is built using Python library PyInstaller. A text file named compile_instructions.txt in the application's source code folder contains instructions to compile the application.

Compilation requires Python and a number of additional libraries to be installed. For details of libraries/versions installed see [Python Libraries](http://wiki.savvy.work/it-procedures/application-deployment-summary/python-libraries) page.

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>