<!-- TITLE: Application Deployment Summary -->


# <span id="title-text">IT Procedures : Application Deployment Summary</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

<div class="table-wrap">

<table class="wrapped confluenceTable"><colgroup><col style="width: 185.0px;"><col style="width: 157.0px;"><col style="width: 140.0px;"><col style="width: 469.0px;"><col style="width: 137.0px;"><col style="width: 268.0px;"><col style="width: 316.0px;"><col style="width: 135.0px;"></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Name</th>

<th class="confluenceTh">Purpose</th>

<th class="confluenceTh">Type</th>

<th class="confluenceTh">Deployment Location</th>

<th class="confluenceTh">Log files</th>

<th class="confluenceTh">Config files</th>

<th class="confluenceTh">Code</th>

<th colspan="1" class="confluenceTh">Databases</th>

</tr>

<tr>

<td class="confluenceTd">

Email Attachement Downloader
</td>

<td class="confluenceTd">Download email attachments from regular emails</td>

<td class="confluenceTd">3rd-party</td>

<td class="confluenceTd">

AWS2-SVR-AP-009

C:\Program Files (x86)\GearMage\Mail Attachment Downloader Pro v2.4

</td>

<td class="confluenceTd">Accessible via GUI</td>

<td class="confluenceTd">N/A</td>

<td class="confluenceTd">N/A</td>

<td colspan="1" class="confluenceTd">N/A</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">

FTP Server

(James D to complete)

</td>

<td colspan="1" class="confluenceTd">Collect files pushed/pulled from various sources via FTP & related file transfer protocols. Meter data, phone recordings, etc.</td>

<td colspan="1" class="confluenceTd">3rd-party</td>

<td colspan="1" class="confluenceTd">MEL-SVR-AP-001</td>

</tr>

<tr>

<td class="confluenceTd">

SavvyDownloaderScheduler

</td>

<td colspan="1" class="confluenceTd">Schedule regular FTP/HTTP downloads</td>

<td colspan="1" class="confluenceTd">Compiled Python console application designed to run continuously. Kicked off by Task Scheduler</td>

<td colspan="1" class="confluenceTd">

MEL-SVR-AP-001

E:\SavvyApps\SavvyDownloadScheduler\dist\SavvyDownloadScheduler

</td>

<td colspan="1" class="confluenceTd">E:\ApplicationLogs</td>

<td colspan="1" class="confluenceTd">Same as deployment location</td>

<td colspan="1" class="confluenceTd">

SVN:

Dev\MarketData\SavvyDownloadScheduler.py

</td>

<td colspan="1" class="confluenceTd">MarketData (R/W)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">SavvyDataLoader</td>

<td colspan="1" class="confluenceTd">Load market data files into the MarketData database</td>

<td colspan="1" class="confluenceTd"><span>Compiled Python console application designed to run continuously. Kicked off by Task Scheduler</span></td>

<td colspan="1" class="confluenceTd">

MEL-SVR-AP-001

E:\SavvyApps\SavvyDataLoader

</td>

<td colspan="1" class="confluenceTd">E:\ApplicationLogs</td>

<td colspan="1" class="confluenceTd">Same as deployment location</td>

<td colspan="1" class="confluenceTd">

SVN:

Dev\MarketData\SavvyDataLoader.py

</td>

<td colspan="1" class="confluenceTd">MarketData (R/W)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">InvoiceDataLoader</td>

<td colspan="1" class="confluenceTd">Load invoice CSV files into the InvoiceLoader database</td>

<td colspan="1" class="confluenceTd"><span>Compiled Python console application designed to run continuously. Kicked off by Task Scheduler</span></td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">MeterDataLoader</td>

<td colspan="1" class="confluenceTd">Load meter data into the MeterDataDB database</td>

<td colspan="1" class="confluenceTd"><span>Compiled Python console application designed to run continuously. Kicked off by Task Scheduler</span></td>

<td colspan="1" class="confluenceTd">

MEL-SVR-AP-001

E:\SavvyApps\MeterDataLoader\MeterDataLoader.exe

</td>

<td colspan="1" class="confluenceTd">E:\ApplicationLogs</td>

<td colspan="1" class="confluenceTd">Same as deployment location</td>

<td colspan="1" class="confluenceTd">

SVN:

Dev\MeterData\MeterData\MeterDataLoader.py

</td>

<td colspan="1" class="confluenceTd">MeterDataDB (R/W)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">pdrLoader (MEL)</td>

<td colspan="1" class="confluenceTd">Load AEMO ElecMMS files into the (MEL) ElecMMS database</td>

<td colspan="1" class="confluenceTd">3rd-party application designed to run continuously. Kicked off by Task Scheduler</td>

<td colspan="1" class="confluenceTd">

MEL-SVR-AP-001

E:\pdrLoader\Lib\pdrLoader.bat

</td>

<td colspan="1" class="confluenceTd">

<span>MEL-SVR-AP-001</span>

E:\pdrLoader\Log

</td>

<td colspan="1" class="confluenceTd">

<span><span>MEL-SVR-AP-001</span>  
</span>

<span>E:\pdrLoader\Lib\</span>pdrloader.properties

</td>

<td colspan="1" class="confluenceTd">N/A</td>

<td colspan="1" class="confluenceTd">ElecMMS (MEL-SVR-DB-002)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">pdrLoader (DC)</td>

<td colspan="1" class="confluenceTd"><span>Load AEMO ElecMMS files into the (DC) ElecMMS database</span></td>

<td colspan="1" class="confluenceTd">3rd-party application runs as service pdrLoader</td>

<td colspan="1" class="confluenceTd">

DC1-SVR-AP-001

E:\pdrLoader\Lib\pdrLoader.exe

</td>

<td colspan="1" class="confluenceTd">

<span>DC1-SVR-AP-001</span>

E:\pdrLoader\Log

</td>

<td colspan="1" class="confluenceTd">

<span><span>DC1-SVR-AP-001</span>  
</span>

<span>E:\pdrLoader\Lib\</span><span>pdrloader.properties</span>

</td>

<td colspan="1" class="confluenceTd">N/A</td>

<td colspan="1" class="confluenceTd"><span>ElecMMS (DC1-SVR-DB-001)</span></td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Web Portal</td>

<td colspan="1" class="confluenceTd">Allow user to manage client data and manually maintained market data etc.</td>

<td colspan="1" class="confluenceTd">Data management tool developed in Django (Python web framework). Runs in Django development server</td>

<td colspan="1" class="confluenceTd">

MEL-SVR-AP-001

Batch file C:\Users\sp.admin\Desktop\Run Web Portal.bat

Runs from code copy in E:\SavvyApps\EnergyAccounting\v0.0.1

</td>

<td colspan="1" class="confluenceTd">N/A (run in console mode if wanting to see log info)</td>

<td colspan="1" class="confluenceTd"><span>E:\SavvyApps\EnergyAccounting\v0.0.1</span></td>

<td colspan="1" class="confluenceTd">

SVN:

Dev\EnergyAccounting\trunk

</td>

<td colspan="1" class="confluenceTd">EnergyAccounting (R/W)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Cost Calculator</td>

<td colspan="1" class="confluenceTd">Calculate invoice</td>

<td colspan="1" class="confluenceTd">Excel spreadsheet template with macros for running calcs and saving results</td>

<td colspan="1" class="confluenceTd">

Current template in

S:\Consulting\Tools\Template\Invoice Validation & Budget

</td>

<td colspan="1" class="confluenceTd">N/A</td>

<td colspan="1" class="confluenceTd">N/A</td>

<td colspan="1" class="confluenceTd">N/A</td>

<td colspan="1" class="confluenceTd">ApplicationsDB (R/W)</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">

Meter Data Extractor

(James C to complete)

</td>

<td colspan="1" class="confluenceTd">Forecast interval meter data and calculate various time-of-use, demand and<br>
other consumption definitions for past and future periods</td>

<td colspan="1" class="confluenceTd">Compiled MATLAB GUI application</td>

<td colspan="1" class="confluenceTd">

MarketData

</td>

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