<!-- TITLE: Reporting Database Loader -->
<!-- SUBTITLE: A quick summary of Reporting Database Loader -->

# <span id="title-text">IT Procedures : Reporting Database Framework</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

### Purpose

A framework has been created to allow quickly and easily creating, maintaining and monitoring reporting databases. A sample reporting database was created for NEM market data using the framework.

The framework is designed to support the progressive development of a reporting database in an environment with a high proportion of business users with strong SQL capabilities. It provides the ability to maintain a complete history of reporting datasets where desirable.

The framework largely automates the creation of tables, views and data update scripts. This is intended to simplify the development task and help achieve a consistent approach. There may be cases where the automatically generated tables and/or update scripts may not be appropriate, in which case the framework is modular to allow modifications.

### Components

The components of the system are:

*   Reporting database - the final database where reporting data is physically persisted and reporting views are created.
*   Staging database - collates data (primarily using views pointing to other databases) for loading into the reporting database
*   SQL Server agent maintenance jobs
*   Python script to script the creation of reporting tables, views and table update stored procs

### Maintenance and Monitoring

The reporting database is refreshed once per day by a SQL Server Agent job (sync_Reporting_Tables_NEM). This calls a stored procedure, which in turn calls a series of stored procedures which each update 1 individual table.

On success or failure the job sends a notification email to the SQL Admin email list for monitoring purposes.

The update scripts write to logging tables as follows:

Merge_Process: 1 record per individual table data update. Logs the process name, target table, process status, number of records inserted/deleted/updated, total records in source view, start/finish time and duration.

Messages: detailed logging of process for debugging purposes. Logs entry time and message.

### Creating new reporting tables

The framework is designed around the following process for adding new reporting data sets:

1.  Reporting analyst identifies the need for a new reporting data set and writes a SQL select statement to return it
2.  Reporting database owner (RDO) reviews and adds to staging database:
    1.  identifies any dimensions that should be broken out as separate tables
    2.  tidies up for consistency with reporting database conventions
    3.  restricts query to the data needed for daily updates where necessary/feasible
    4.  creates views in staging database
3.  RDO runs Python scripts (for each view) with appropriate arguments to produce a SQL Script that:
    1.  creates a reporting table with fields matching those of the source view plus an identity field, ActiveFrom date/time and ActiveTo date/time for maintenance of history
    2.  creates a view exactly matching those of the source view but pointing to the new reporting table and showing currently active records only
    3.  creates a stored proc for the maintenance of the new reporting table by synchronising with the source view in the staging database
4.  RDO schedules the data refresh using SQL Server Agent.

### Technical Details

The reporting database is named Reporting and is located on MEL-SVR-DB-002\. It contains views (for most reporting), tables (where version history is required), stored procs used to refresh the various data tables and sp_SyncAllTables_NEM which sequences the refresh of the tables. Views in Reporting point only to tables also in Reporting.

The staging database is named Report_Staging (MEL-SVR-DB-002). It consists entirely of views at the moment. Views can point to Reporting database tables/views (e.g. dimension tables) as well as to other databases.

The SQL Server Agent job that refreshes reporting data is named sync_Reporting_Tables_NEM and runs on MEL-SVR-DB-002.

Python script to automate SQL script generation is named makeReportTable.py and is located in SVN repository under Dev\MarketData\.

###### Python script - parameters

A sample file used to create tables for the existing NEM reporting tables can be found in create_NEM_Reporting_Model.py in SVN \MarketData

For each table it calls a simple function getSQL(db,schema,view,key_fields,version,remove_if_not_found) which shows the usage of the tool to produce a single SQL script

The arguments to getSQL are as follows:

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Argument</th>

<th class="confluenceTh">Usage</th>

</tr>

<tr>

<td colspan="1" class="confluenceTd">db</td>

<td colspan="1" class="confluenceTd">Name of database containing the source view e.g. 'Report_Staging'</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">schema</td>

<td colspan="1" class="confluenceTd">

Name of database schema containing the source view e.g. 'NEM'.

The new reporting table will also be created under this schema in the Reporting database.

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">view</td>

<td colspan="1" class="confluenceTd">

Name of the source view e.g. 'SpotPriceDemand_30min'.

The new reporting table will be the same with '_Vers' appended

The new reporting view will have the same name.

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">key_fields</td>

<td colspan="1" class="confluenceTd">

A list of field names constituting a natural key for the reporting table e.g. ['Region', 'SettlementDate']

A unique non-clustered index will be created on this combination of fields in the new table if version is set to False

The source view must not contain multiple records with the same combination of values for these fields or the update will fail

If a record in the source view does not match any existing record in the reporting table a new record will be created. If a match is found then the values in the source view will be treated as a new version of the record and an update will occur.

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">version</td>

<td colspan="1" class="confluenceTd">

True if each version of the data should be maintained in the reporting table.

False if only the current version of the data should be maintained

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">remove_if_not_found</td>

<td colspan="1" class="confluenceTd">

Determines the behaviour when data is found in the reporting table but not the source view.

If True, then remove/deprecate the reporting record.

If False, then do not remove/deprecate the reporting record.

This argument is important when the source view may not contain a full set of data (e.g. for spot prices source view might return only last 7 days of data to maximise update performance, as nothing prior to that date should have changed)

</td>

</tr>

</tbody>

</table>

</div>

### Notes

The automatic SQL script generation won't create foreign keys on reporting tables. These should be added manually when required.

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>