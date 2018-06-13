<!-- TITLE: Meter Data Loader -->
<!-- SUBTITLE: A quick summary of Meter Data Loader -->


# <span id="title-text">IT Procedures : MeterDataLoader</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

### Purpose

The MeterDataLoader application is a tool to process interval meter data files and load into the MeterDataDB database. The application supports industry-standard NEM12 and a fully flexible range of CSV formats. It is structured to allow the addition of extra handlers for other file types if required.

As at May 2017 the main 15- and 30-minute meter data tables contain over 200m records representing meter data for around 2100 meters.

### Technical Details

This application is a SavvyPlus-developed console application written in Python.

It runs on MEL-SVR-AP-001 and is started by a scheduled task. It is designed to run continuously.

The application is located at E:\SavvyApps\MeterDataLoader\MeterDataLoader.exe and writes log files to E:\ApplicationLogs

The application writes to and reads from the MeterDataDB database. Configuration table is MeterDataLoaderJobs and file processing records are stored in MeterDataLoaderFiles

### Operation

On opening, the application reads a list of loading jobs from table MeterDataLoaderJobs. Each job specifies a source folder, a handler and various parameters to pass to it, an error folder for failed files and archive folder for successfully processed files. It also specifies a retention time for successfully processed files.

During operation the application continually cycles through the following steps:

1.  Refreshes the jobs list if it has been longer than the specified time interval (e.g. 60seconds) since last done
2.  Performs a directory listing for each source folder if it has been longer than the specified time (e.g. 5 seconds) since last done, and identifies files matching each job's file name mask
3.  Determines the priority order for processing files based on each job's priority rank
4.  Processes the highest-priority file in the queue  

    1.  passes the file name/location to the specified handler
    2.  if handler returns successfully, move file to archive folder
    3.  if handler returns and error, move file to error folder
    4.  write result to MeterDataLoaderFiles table
5.  Purge archive files according to each job's file mask and retention time setting

### Monitoring and Troubleshooting

There is no explicit monitoring on this application but performance can be checked by looking at the various Queue folders for a buildup of files.

In normal operation the application is highly reliable and re-start is not required.

For advanced trouble-shooting consult the log file, or run the application from a dos box to see error messages produced.

### Application Configuration

The following parameters can be set in the config file MeterDataLoader.cfg located in the deployment folder:

Database Connection

*   odbcconnectionstring: ODBC database connection string to connect to database
*   retry_time_seconds: time (seconds) to wait between database connection re-tries (e.g. 5)

Refresh Times

*   source_locations_refresh_seconds:  time interval (seconds) between refreshing the list of source locations to load files from (e.g. 60)

*   source_files_refresh_seconds: time interval (seconds) between polling the source folders to look for new files (e.g. 5)

*   archive_purge_delay_minutes: time interval (minutes) at which to purge archive folders (e.g. 1)

### Configuring Meter Data Loading Jobs

Jobs are managed through the MeterDataLoaderJobs table. The fields are as follows:

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

<td colspan="1" class="confluenceTd">commodity</td>

<td colspan="1" class="confluenceTd">Text to indicate commodity (e.g. ELEC) for which metering data is loaded.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">organisation</td>

<td colspan="1" class="confluenceTd">Text to indicate which organisation/client the loaded data is supposed to be for.</td>

</tr>

</tbody>

</table>

</div>

######   Existing Handlers

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Handler</th>

<th class="confluenceTh">Role</th>

</tr>

<tr>

<td class="confluenceTd">spmdf_handler</td>

<td class="confluenceTd">Highly configurable handler to load interval meter data in just about any CSV-like format. See detail below.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">move_only</td>

<td colspan="1" class="confluenceTd">File is moved from source to archive folder without further processing</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">unzip</td>

<td colspan="1" class="confluenceTd">Unzips the file in-place i.e. extracts the contents of the zipped file to the same location.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">nem12_handler</td>

<td colspan="1" class="confluenceTd">Load meter data in NEM12 format.</td>

</tr>

</tbody>

</table>

</div>

###### spmdf_handler

This handler can be used to process a large number of CSV files and variants without modifying the original file so that ongoing meter data feeds in any CSV-like format can be accepted.

The processing steps can be summarised as follows:

> ###### Raw format → SPMDF format → Staging table → Final table

To work with a new file format you use the flexibility of the MeterDataLoader's (and pandas' read_csv) functions to map the original format to an acceptable SPMDF format by passing appropriate parameters to the handler. This generally involves selecting, adding & renaming columns, and sometimes applying certain rules to particular columns as well as stripping off header and footer information and interpreting dates.

The requirements of the target SPMDF format are as follows:

1.  Valid field names (case-sensitive) are: MeterRef, NMI, StreamRef, MeterSerialNumber, Date, Time, PeriodID, Timestamp, TimestampType, IntervalLength, Net_KWH, Net_KVARH, Exp_KWH, Imp_KWH, Exp_KVARH, Imp_KVARH, KW, KVA, MDPUpdateDateTime, QualityCode
2.  IntervalLength field must exist and be populated with values of 15 or 30
3.  Meter reading time must be specified as one of Timestamp+TimestampType, Date+PeriodID, or Date+Time+TimestampType
4.  Meter must be specified either as MeterRef or as NMI+StreamRef
5.  At least one of the following fields must be supplied: Net_KWH, Net_KVARH, Exp_KWH, Imp_KWH, Exp_KVARH, Imp_KVARH, KW, KVA
6.  QualityCode must be present and contain only the following values: ,'A','E','F','I','S','X'
7.  All Exp_KWH, Imp_KWH, Exp_KVARH, Imp_KVARH and KVA values must be non-negative

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Parameter Name</th>

<th class="confluenceTh">Usage</th>

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

<td colspan="1" class="confluenceTd">fixed_column_vals</td>

<td colspan="1" class="confluenceTd">

Creates additional columns that contain a particular fixed value. Uses include:

*   to specify IntervalLength when not provided but you know the resolution to expect (30 or 15)
*   to specify QualityCode when not provided (e.g. to assign unknown quality code 'X')
*   to specify the TimestampType i.e. PE (period-ending) or PS (period-starting)

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">truncateNMI</td>

<td colspan="1" class="confluenceTd">Truncates the MeterRef or NMI field to the first 10 characters. Use if the NMI/MeterRef has a checksum digit or other information appended.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">map_col_names</td>

<td colspan="1" class="confluenceTd">Dict of source and target column names. Use to convert the supplied column names to valid SPMDF field names.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">flip_signs</td>

<td colspan="1" class="confluenceTd">List of field names whose values should have their sign flipped. Use if e.g. import kwh in file is shown as a negative value.</td>

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

<td class="confluenceTd">{'parse_dates':['Timestamp'],'dayfirst':True}</td>

<td class="confluenceTd">Treat the field named Timestamp as a date/time field. Assume dd/mm rather than mm/dd. This is a basic set of parameters where the source files are already in SPMDF format.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">{'usecols':['NMI','REPORT_DATE','REPORT_TIME','KVARH_CON','KVARH_GEN','KWH_CON','KWH_GEN'],'parse_dates':['REPORT_DATE'],'dayfirst':True,'header':0,'fixed_column_vals':{'IntervalLength':15,'TimestampType':'PE','QualityCode':'X'},'map_col_names':{'NMI':'MeterRef','REPORT_DATE':'Date', 'REPORT_TIME':'Time', 'KVARH_CON':'Exp_KVARH', 'KVARH_GEN':'Imp_KVARH', 'KWH_CON':'Exp_KWH', 'KWH_GEN':'Imp_KWH'}}</td>

<td colspan="1" class="confluenceTd">ERM meter data format (by NMI). Select a subset of the columns only. Interpret REPORT_DATE as a date/time with day before month. Headings are in row 0 (first row). Add IntervalLength field (value 15), TimestampType (period-ending), QualityCode (X). Map column names NMI→MeterRef, REPORT_DATE→Date, REPORT_TIME→Time, KVARH_CON→Exp_KVARH etc.</td>

</tr>

</tbody>

</table>

</div>

### Compiling

The application is built using Python library PyInstaller. A text file named compile_instructions.txt in the application's source code folder contains instructions to compile the application.

Compilation requires Python and a number of additional libraries to be installed. For details of libraries/versions installed see [Python Libraries](Python-Libraries_51675342.html) page.

### Notes

When spmdf_handler is used:

*   data loads into table SPMDF_Staging
*   stored proc MergeSPMDF_Staging is called by the MeterDataLoader
*   MergeSPMDF_Staging loads data for each NMI-StreamRef is loaded into IMD_Staging table
*   MergeIMD_Staging is then called to merge all meter data straight away into final tables

When nem12_handler is used:

*   data loads into a series of staging tables NEMMDF_Staging_*
*   on an hourly schedule stored proc MergeAllNEMMDF_Staging_Files runs, calling MergeNEMMDF_Staging once per source file
*   by default data is loaded at NMI resolution only, but if NMI-X exists in IMD_MeterPoint then the individual meter's data will also load into the final tables. So e.g. if VAAA000123-1 exists in IMD_MeterPoint, and data is loaded for VAAA000123 with E1,E2,Q1,Q2 then the aggregate of E1E2Q1Q2 will load as VAAA000123 and the aggregate of E1Q1 will load as VAAA000123-1
*   MergeNEMMDF_Staging aggregates data <u>with previously loaded streams</u> and loads into IMD_Staging
*   MergeIMD_Staging is called to merge all meter data into final tables

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>