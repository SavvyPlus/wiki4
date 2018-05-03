<!-- TITLE: Databases -->
<!-- SUBTITLE: A quick summary of Databases -->


# <span id="title-text">IT Procedures : Databases</span>

</div>

<div id="content" class="view">


<div id="main-content" class="wiki-content group">

### Servers

There are 2 SQL Servers currently in operation, one in the Melbourne (MEL) server room and the other in the Data Centre (DC1).

The SQL servers are named for the VMs they run on:

*   MEL-SVR-DB-002 - hosts production systems currently
*   DC1-SVR-DB-001 - intended to host prod systems in future

### Database List and Description

<div class="table-wrap">

<table class="wrapped relative-table confluenceTable" style="width: 100.0%;"><colgroup><col style="width: 28.284%;"><col style="width: 7.69231%;"><col style="width: 48.4024%;"><col style="width: 15.6213%;"></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Database(s)</th>

<th class="confluenceTh">Server</th>

<th class="confluenceTh">Description</th>

<th class="confluenceTh">Additional Info</th>

</tr>

<tr>

<td class="confluenceTd">MarketData</td>

<td class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td class="confluenceTd">Collection of market information, largely in raw formats. Designed to facilitate automated collection of market data, and remove the application of business logic interpreting the data to a later stage.</td>

</tr>

<tr>

<td class="confluenceTd">MeterDataDB</td>

<td class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td class="confluenceTd">

Supports (and populated by) the MeterDataLoader application.

Holds interval meter data for all clients. Used by production reports and systems for all clients.

</td>

</tr>

<tr>

<td class="confluenceTd">EnergyAccounting</td>

<td class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td class="confluenceTd">

Web portal database. Tables created/managed by Django web framework. Contains all production client data such as meters, sites, groupings, attributes etc.

</td>

</tr>

<tr>

<td class="confluenceTd">InvoiceLoader</td>

<td class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td class="confluenceTd">

Supports the InvoiceLoader application used to load invoices for all clients (except CSR).

Stores CSV invoice files in a raw format and allows users to configure the application to convert to a standardised format.

Used by production reports.

</td>

<td class="confluenceTd"><span>The stored proc RawEDI_To_Staging uses dynamic SQL. This should only be runnable by users on their own login to avoid possibility of circumventing database permissions.</span></td>

</tr>

<tr>

<td class="confluenceTd">ElecMMS</td>

<td class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td class="confluenceTd">

Replica of AEMO's Electricity Market Management System database based on public downloads and feeds from retailer OPG.

</td>

<td class="confluenceTd">Very large database. Based on old EMMS data model version</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">ApplicationsDB</td>

<td colspan="1" class="confluenceTd">MEL-SVR-DB-002</td>

<td colspan="1" class="confluenceTd">Home for various MATLAB/spreadsheet-based applications to write results to including Cost Calculator and Spot Forecasting. Many designed but not yet used by applications/users.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">CSR</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">Supports production reporting for client CSR.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">CSR_Dev</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">???</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">CSR_Restored</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">???</td>

</tr>

<tr>

<td class="confluenceTd">Billing</td>

<td class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td class="confluenceTd">Early attempt to collect some market data.</td>

<td class="confluenceTd">NOT REQUIRED</td>

</tr>

<tr>

<td class="confluenceTd">

CBA

ClientData

TasWater

Wesfarmers

</td>

<td class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td class="confluenceTd">Created to hold client data for particular clients including CBA, PA, TasWater and Wesfarmers. Data may be useful for future projects but not actively used</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">OperationalReporting</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">

Prototype to try to develop a reporting schema, where reporting structures are created without persisting the data.

Some production reports (e.g. Market News) may use this.

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">PhoneBuddy</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">Database created to store phone plans/billing information to support the PhoneBuddy mobile phone application. Not in use.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">

Reporting

<span>Report_Staging</span>

</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">

Reporting is a prototype reporting database containing market data tables. Report_Staging is a staging environment used to populate it.

Some production reports may use Reporting.

Reporting is self-contained (i.e. no views etc. referencing other databases). It is maintained by a series of auto-generated stored procs that read data from Report_Staging.

Report_Staging consists only of views to other databases (including Reporting).

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">ReportingAcceleon</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">Attempt by consultants Acceleon to build a market data reporting database.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">

ReportServer

<span>ReportServer$SQLSVR01</span>

<span>ReportServer$SQLSVR01TempDB</span>

<span>ReportServerTempDB</span>

</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">Support SQL Server Reporting Services (SSRS)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">SSISDB</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">Supports SQL Server Integration Services (SSIS)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">UserDev</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">

Analysts/users given complete access to this database to assist in prototyping reporting tables etc.

Many production reports may point to this database.

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">VisyEnergyManagement</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">

Prototype of system for Visy to collect confidential gas data using the SavvyDataLoader application.

Not currently used.

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">WPT</td>

<td colspan="1" class="confluenceTd"><span>MEL-SVR-DB-002</span></td>

<td colspan="1" class="confluenceTd">Supports various systems used for running WPT's trading operation and reporting to OPG including mark-to-market, position reporting, market settlements, contract settlements, demand reporting etc.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">ElecMMS</td>

<td colspan="1" class="confluenceTd">DC1-SVR-DB-001</td>

<td colspan="1" class="confluenceTd">Replica of AEMO's EMMS database. This copy intended to keep only a short history of data. A stored proc runs each day to purge older data and maintain size.</td>

<td colspan="1" class="confluenceTd">Based on recent version of EMMS data model.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">SecretServer</td>

<td colspan="1" class="confluenceTd"><span>DC1-SVR-DB-001</span></td>

<td colspan="1" class="confluenceTd">Supports Thycotic Secret Server 3rd-party application used internally for password management.</td>

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