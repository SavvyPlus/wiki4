<!-- TITLE: Email Attachment Downloader -->
<!-- SUBTITLE: A quick summary of Email Attachment Downloader -->

# IT Procedures : Email Attachment Downloader


</div>

<div id="content" class="view">



<div id="main-content" class="wiki-content group">

### Purpose

We use a 3rd-party software package that can be configured to collect attachments from regular emails.

### Technical Details

The software is Mail Attachment Downloader PRO Server v2.4 by GearMage.

Installation folder is "C:\Program Files (x86)\GearMage\Mail Attachment Downloader Pro v2.4"

It runs as a service on AWS2-SVR-AP-009.

### Configuration

To configure the application use the GUI provided (MailAttachmentDownloader.exe). Use "Run as administrator" to open the GUI if you need to make any changes - it needs permission to uninstall/install the service.

Online documentation is available [https://gearmage.com/buymaildownloader.html](https://gearmage.com/buymaildownloader.html)

### Notes:

*   The GUI is quite unintuitive, especially when running as a service.
*   There are some limitations around using basic/advanced filters while running as a service. Use global filters only.
*   When changing/adding filters always reset the _Start Date_ on all existing filters to the current date, otherwise on restart it will re-process all previous emails.
*   Basic steps to add/modify filters are:

1.  Uninstall service (on service tab)
2.  Add the new filter or modify an existing one (global filters tab)
3.  Modify all filters by setting the Start Date to today to prevent re-processing of old emails
4.  In the Email accounts combo box select multiple@multiple. In the pop-up choose all the accounts the service needs to download from.
5.  On the Service tab press Install service to start it running.

<br>

*   The _Filename matches_ box on the global filters editor uses Microsoft Visual C++ regular expression grammar, not dos-style filename matching i.e. *.xlsx will not do what you expect. For details see [https://msdn.microsoft.com/en-us/library/bb982727.aspx](https://msdn.microsoft.com/en-us/library/bb982727.aspx)

</div>

</div>

</div>

<div id="footer" role="contentinfo">

<section class="footer-body">


</section>

</div>

</div>