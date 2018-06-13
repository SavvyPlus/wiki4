<!-- TITLE: Bulk Uploaders -->
<!-- SUBTITLE: A quick summary of Bulk Uploaders -->


# <span id="title-text">IT Procedures : Bulk Uploaders</span>

</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">


### Overview

Within the web portal there is functionality for bulk management (creation/update) of certain client energy data.

The user populates a spreadsheet template with the data to be added/changed, and a loading process applies a series of business logic rules to validate and add or create the data entities.

Bulk loaders exist for:

*   Sites
*   Service Points
*   Service Point Grouping Assignment
*   Service Point Attribute Assignment
*   Service Point Agreement Assignment

### Usage

Bulk uploaders are accessible within the web portal under the Loading app→Bulk Uploaders.

To perform a new bulk upload, use "Add bulk upload".

*   Select the completed (and saved) template file with the data to load
*   Select the template type
*   Give a description of the data you're trying to load
*   Hit Save and Continue Editing to run the bulk upload and see the results.

Clicking on an earlier upload run will allow you to see the outcomes:

*   A series of messages will be displayed which may be described as either Info, Warning or Error. Each may show a line number, which specifies which line of the template file it refers to

Templates for each type of upload are available at ...

The business logic used to validate, create and/or modify data is best described by reviewing the relevant source code in the file bulkupload_handlers.py. Technically capable users have found this fairly readable.

### Populating the template

Detailed description of what goes in the templates...

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">


</section>

</div>

</div>