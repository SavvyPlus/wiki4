<!-- TITLE: Data Bus And File Storage -->
<!-- SUBTITLE: A quick summary of Data Bus And File Storage -->

# <span id="title-text">IT Procedures : Data Bus & File Storage</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

### Purpose

This layer is designed to:

*   provide appropriate retention of raw data files
*   allow queuing of file processing tasks
*   allow monitoring of file processing systems for queue buildup and file failures
*   cater for a modular design of data collection and file processing layers
*   facilitate loading of ad-hoc files by users

### Design

At a high level this component uses the server's file system to create:

*   Queue folder, in which each subfolder represents a processing queue for a particular application or report type
*   Errors folder, in which each subfolder is a location for files that fail processing to be placed
*   Archive folder, in which subfolders provide a temporary or permanent storage location for files that have been processed successfully (i.e. loaded into a database).

This structure exists for meter data, market data and invoice data.

The physical folders currently exist on MEL-SVR-AP-001\. Mirroring has been set up that synchronises these folders to DC1-SVR-AP-001.

File shares exist that expose the folders to appropriate users. This allows users to load ad-hoc files, view/investigate/re-process failed files, see the processing queues, view archive folders.

### Exceptions

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">


</section>

</div>

</div>