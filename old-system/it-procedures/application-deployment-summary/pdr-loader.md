<!-- TITLE: Pdr Loader -->
<!-- SUBTITLE: A quick summary of Pdr Loader -->

<div id="page">

<div id="main" class="aui-page-panel">

<div id="main-header">



# <span id="title-text">IT Procedures : pdrLoader</span>

</div>

<div id="content" class="view">


<div id="main-content" class="wiki-content group">

### Purpose

This AEMO application is used to load their market data reports into a replica of their Electricity Market Management (EMMS) database.

### Technical Details

The pdrLoader is a Java application that can also be configured to run as a windows service.

We run 2 instances.

MEL-SVR-AP-001 runs one instance used to maintain database ElecMMS on MEL-SVR-DB-002 - runs as scheduled task

DC1-SVR-AP-001 runs another instance used to maintain ElecMMS database on DC1-SVR-DB-002 - runs as service

### Documentation

AEMO have a range of documents describing the pdrLoader and other Data Interchange software.

### Configuration

The application is configurable via the pdrLoader.properties configuration file.

To set loading behaviour for indivudal reports a separate application Replication Manager can be installed and used. See AEMO documentation.

### Maintenance

The ElecMMS data model is updates twice per year by AEMO. To stay up to date with the latest version the updates should be applied within 5-6 months of becoming available. Database update scripts and instructions are published by AEMO. AEMO support Data Interchange for Oracle or SQL Server.

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">



</section>

</div>

</div>