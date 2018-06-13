<!-- TITLE: Web Portal -->
<!-- SUBTITLE: A quick summary of Web Portal -->

# <span id="title-text">IT Procedures : Web Portal</span>

</div>

<div id="content" class="view">


<div id="main-content" class="wiki-content group">

### Purpose

The web portal provides a data management interface to internal users with data management functionality for client and market energy data. It provides basic CRUD operations for a range of data entities but with a focus on those relevant to energy billing. It is used to manage the sites, meters, supply contracts, regulated and market tariffs, loss factors etc. for all clients that we perform bill validation, cost outlooks, accruals, budgeting etc. for. It also holds wholesale contracts, powerBI report permissions, market news and other market information requiring manual user maintenance. It also provides functionality to create and/or update items in bulk by uploading spreadsheet templates - this applies to the most heavily used items such as customer sites and attributes.

### Technical Details

The web portal is built using Django, a Python web application framework. Django was selected partly because of the power of its admin site functionality - the web portal uses this exclusively to avoid needing a web developer to implement.

It is accessible while connected to our network at http://webportal.savvy.work/admin/

The web portal is hosted on MEL-VDT-001. It runs in the Django development server and has not been deployed to a production web server. Running in the development server hasn't caused any issues running internally with a small number of users.

The dev server runs from a working copy of the source code. The code is in E:\SavvyApps\EnergyAccounting\v0.0.1\. It is started by a scheduled task.

### Code structure

The source code for the web portal [https://github.com/SavvyPlus/Webapp_Django.git](https://github.com/SavvyPlus/Webapp_Django)

Within that folder it is structured as several discrete apps that basically correspond to the various blocks of items appearing in the main site administration screen.

A summary of these is as follows

<div class="table-wrap">

<table class="confluenceTable"><colgroup><col style="width: 136.0px;"><col style="width: 89.0px;"><col style="width: 1062.0px;"></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Application</th>

<th class="confluenceTh">Status</th>

<th class="confluenceTh">Description</th>

</tr>

<tr>

<td colspan="1" class="confluenceTd">EnergyAccounting</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">

Contains settings that flow through the site such as database connections, time zone and lanaguage settings, security settings, urls etc.

The key file here is settings.py

</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">organisations</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Management of client organisations, sites, service points, reporting groups and attributes etc.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">rates</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Management of retail and network supply agreements, regulated & contestable tariffs, market billing parameters (e.g. enviro scheme percentages), loss factors, units of measure etc.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">services</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Billing configuration information. Describing the types of billing arrangements and what kinds of bill components apply to each.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">EDMR</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Base models used by the other apps</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">invoice</td>

<td colspan="1" class="confluenceTd">Alpha</td>

<td colspan="1" class="confluenceTd">Preliminary design of structures for managing invoices and related info. Not in use.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">loading</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Provides interfaces for managing sites, meters, attributes etc. in bulk using spreadsheet templates.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">market_news</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">User entry of news articles to support powerBI reports.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">NEM</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Management of NEM generator information feeding generator reports.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">PowerBI</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Permissions management for powerBI reports.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">tools</td>

<td colspan="1" class="confluenceTd">Alpha</td>

<td colspan="1" class="confluenceTd">Preliminary design of user interface for running network tariff reviews etc. Not in use.</td>

</tr>

<tr>

<td colspan="1" class="confluenceTd">wholesale</td>

<td colspan="1" class="confluenceTd">Production</td>

<td colspan="1" class="confluenceTd">Management of wholesale electricity contracts - swaps, caps, etc.</td>

</tr>

</tbody>

</table>

</div>

### Troubleshooting

TBA 

### Deployment

The web portal has 3 different instances all autoamiucally deployed by jenkins.savvy.work

<div class="table-wrap">

<table class="confluenceTable"><colgroup><col style="width: 136.0px;"><col style="width: 89.0px;"><col style="width: 90.0px;"><col style="width: 1062.0px;"></colgroup>

<tbody>

<tr>

<th class="confluenceTh">Hosting </th>

<th class="confluenceTh">Addresss</th>

<th class="confluenceTh">Domain</th>

<th class="confluenceTh">Description</th>

</tr>

<tr>

<td colspan="1" class="confluenceTd">Local Windows Desktop MEL-VDT-001</td>

<td colspan="1" class="confluenceTd">MEL-VDT-001 </td>

<td colspan="1" class="confluenceTd">http://webportal.savvy.work/admin/</td>

<td colspan="1" class="confluenceTd">

It contain the Production Webportal, the web portal is connected to the production MS SQL server and writes to EnergyAccounting DB 

</td>

</tr>

<tr>
<td colspan="1" class="confluenceTd">AWS EC2</td>

<td colspan="1" class="confluenceTd">TBA</td>

<td colspan="1" class="confluenceTd">http://staging.savvy.work/</td>

<td colspan="1" class="confluenceTd">

This machine is hosted in AWS t2.small server , it can be access via RDP and writes to a SQL express server on RDS inside the Webportal Pub VPC 

</td>

</tr>

<tr>
<td colspan="1" class="confluenceTd">AWS EC2</td>

<td colspan="1" class="confluenceTd">TBA</td>

<td colspan="1" class="confluenceTd">http://test.savvy.work/</td>

<td colspan="1" class="confluenceTd">

This machine is hosted in AWS t2.micro server , it can be access via RDP and writes to a SQL express server on RDS inside the Webportal Pub VPC 

</td>

</tr>
</tbody>

</table>

</div>

</div>

</div>

</div>

<div id="footer" role="contentinfo">


</div>

</div>