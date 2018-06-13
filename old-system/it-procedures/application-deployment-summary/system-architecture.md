<!-- TITLE: System Architecture -->
<!-- SUBTITLE: A quick summary of System Architecture -->
# <span id="title-text">IT Procedures : System Architecture</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

At a high level, the data flow is set out in the table below.

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup>

<tbody>

<tr>

<th class="confluenceTh">System Layer</th>

<th class="confluenceTh">Activity</th>

<th class="confluenceTh">Key Components</th>

</tr>

<tr>

<td class="confluenceTd">Data Collection Layer</td>

<td class="confluenceTd">

Data is collected via various channels:

*   Regular emailed reports
*   Passive & active (S)FTP transfers
*   FTP/HTTP downloads
*   Manually by users

</td>

<td class="confluenceTd">

*   Email Attachment Downloader
*   SavvyDownloadScheduler
*   FTP Server
*   User-accessible file shares

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Data Bus & File Storage Layer</td>

<td colspan="1" class="confluenceTd">

*   Files are queued and prioritised for processing.
*   Processed files are archived and retention policies applied.
*   File transfers between MEL and DC environments take place

</td>

<td colspan="1" class="confluenceTd">

*   File system
*   Archiving/cleanup scripts
*   Folder synchronisation software

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Data Loading Layer</td>

<td colspan="1" class="confluenceTd">

*   Files are processed and data loaded into system
*   Error files are set aside for reprocessing and further review
*   Version control of data is applied
*   Monitoring of data feeds takes place

</td>

<td colspan="1" class="confluenceTd">

*   SavvyDataLoader
*   MeterDataLoader
*   InvoiceLoader
*   pdrLoader
*   Monitoring jobs

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Database Layer</td>

<td colspan="1" class="confluenceTd">

*   Data is stored in relational form
*   Views are applied to:
    *   combine similar data from multiple sources
    *   provide more user-friendly formats for operational tasks
*   Functions, stored procedures and views for:
    *   monitoring
    *   data verification and cleansing
    *   collating inputs for applications

</td>

<td colspan="1" class="confluenceTd">

Key databases:

*   MarketData
*   MeterDataDB
*   EnergyAccounting
*   InvoiceLoaderDB
*   ElecMMS
*   ApplicationsDB

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Data Management and Application Layer</td>

<td colspan="1" class="confluenceTd">

*   Manual data management tasks performed via web portal GUI
*   Bulk data uploads via templates
*   Budgets, cost outlooks, invoice validation, NTRs
*   Meter data forecasting & aggregation

</td>

<td colspan="1" class="confluenceTd">

*   Web Portal
*   Cost Calculator
*   NTR Calculator
*   Spot Forecasting
*   Meter Data Extractor

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Reporting ETL Layer</td>

<td colspan="1" class="confluenceTd">

*   Preparation of flat, convenient reporting tables and views
*   Recording of data change history

</td>

<td colspan="1" class="confluenceTd">

*   MakeReportingTable scripts
*   Report_Staging database
*   Reporting database

</td>

</tr>

</tbody>

</table>

</div>



</div>

<div class="pageSection group">

<div class="pageSectionHeader">

## Attachments:

</div>

A visual representation of the system is shown in the figure below:


  <div class="pageSection group">
                  

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>
