<!-- TITLE: WPT Trading Operations: Settlements -->
<!-- SUBTITLE: A quick summary of WPT Trading Operations: Settlements -->



WPT Trading Operations : Settlements
====================================

Created by James Cheong, last modified on Jul 13, 2016

Settlement typically occurs once a week with each counterparty. However, due to public holidays, there are occasional weeks where settlement occurs twice. Details of the NEM settlement calendar can be found by in [S:\\Wholesale Power Trading\\Settlements]().

Macquarie bank
==============

Macquarie Bank is the calculation agent for transactions with WPT, thus WPT's role in the settlement process is to confirm that the received invoice amount is correct and to pay the invoice if WPT is the designated payer.  
Typically one or two business days before the Final Statement date, Macquarie Bank will send an invoice to []().  
Open the PDF invoice from Macquarie Bank. Check the net settlement amount, payment date and paying party are correct. The settlement amount can be checked using the Macquarie Bank Settlement Spreadsheet described [here]() and the SQL database query discussed [here]().  
Once confirmed correct, save a copy of the invoice under:  
[S:\\Wholesale Power Trading\\Settlements\\Macquarie Bank\\Invoice]().

Spreadsheet
-----------

Open the following spreadsheet:  
[S:\\Wholesale Power Trading\\Settlements\\Macquarie Bank\\Settlements with Macquarie Bank - with VBA.xlsm](#)  
Click the "_Get Data"_ button in the "_Weekly Settlement_" sheet, to update the half hourly pool price and contract data. The button is located around Cell A1.  
Compare this spreadsheet with the invoice. Look on the invoice for the "Payment Date", and find that corresponding date in the spreadsheet, under column _Payment Date_ (Column E). Once located, scroll across to the column named _Total CFD_ (Column O). The amount listed here should correspond with the total amount on the invoice.  
A positive _Total CFD_ amount on the spreadsheet indicates that Macquarie Bank will pay WPT.  
A negative _Total CFD_ amount on the spreadsheet indicates that WPT will pay Macquarie Bank.  
Once this amount has been confirmed, save the spreadsheet and conduct the next check using the database query discussed [here]().

Database
--------

Connect to the MEL-SVR-DB-002 SQL database using an appropriate version of SQL Server Management Studio.  
Run the following view \[WPT\].\[dbo\].\[MBL\_Weekly\_CFD\] by the following actions:

*   Click on _WPT_ => _Views_ => _dbo.MBL\_Weekly\_CFD_.
*   Right click and choose "_Select Top 1000 Rows"_.
*   A new window will open with some auto generated script. Append the following at the end of the auto generated script: "Order by code"
*   Rerun the query by pressing F5.

This query will produce a similar report to that found in the Settlements spreadsheet.  
Find the corresponding invoice date under column _Payment Date_. Highlight this row by clicking on the row number on the first column of the report, and then scroll across to find the column named _Total CFD_. This amount should match the invoice amount and the amount calculated by the spreadsheet in the previous [section]().  
A positive _Total CFD_ amount on the database report indicates that Macquarie Bank will pay WPT.  
A negative _Total CFD_ amount on the database report indicates that WPT will pay Macquarie Bank.  
Should neither of these amounts match, flag this and forward it to the Head of Trading Operations. Ensure that payment is not made if it is incorrect.

Payment
-------

Reply to the email from Macquarie Bank containing the invoice to confirm that all details are correct. A short email confirming the amount payable, the payer and the payment date is sufficient.  
If the net settlement amount owing is to be paid _by_ WPT (negative number in spreadsheet and database report), then put in a bank transaction to be received by Macquarie Bank 2 days prior to the Payment Date.  
If the amount owing is to be paid _to_ WPT, then nothing further needs to be done.

Online Power and Gas
====================

WPT is the calculation agent for transactions with OPG, thus it has to prepare and issue the invoice according to the NEM Settlement calendar.  
The main components to be invoiced are:

*   Weekly Contract for Difference for Load Following Hedge
*   Weekly Adjustment for Load Following Hedge due to 20 and 30 week revisions
*   Monthly Credit Support Facility Fee (due before the last business day of the month if applicable)
*   High Growth Load Adjustment (payable in the settlement week when Final Settlement Data for the last day of the month has come through, when applicable)
*   20 and 30 week revisions for the High Growth Load
*   Monthly Increased/Reduced Load Premium if actual load falls outside forecasted thresholds (when applicable)

The invoice needs to be generated on the date of the "Final Statement". This will typically occur in the early afternoon, after the Final Settlement Data from AEMO has arrived in [](). The steps to calculate the invoice amount and to generate the invoice will be described in the following sub sections.

Settlement Week Finder
----------------------

Open the following spreadsheet to identify the appropriate revision week numbers for the current Payment Date:  
[S:\\Wholesale Power Trading\\Settlements\\Online Power & Gas\\Settlement Week Finder.xlsx]()  
Select the appropriate Payment Date in the dropdown list in Cell Q9.  
The relevant NEM Weeks will be displayed. Take note of these week numbers when calculating the invoice components.  
Cells Q15 to Q17 will also indicate any end of month adjustments that need to be made for the High Growth Load Adjustment or Increased/Reduced Load Premium, and the appropriate revision (Final, 20 Wk, 30 Wk).

Setup
-----

Open the folder for OPG Settlements:  
[S:\\Wholesale Power Trading\\Settlements\\Online Power & Gas]()  
Create a copy of the latest folder, and save it to the directory specified above.  
Rename the folder to be the Payment Date of the invoice, using the format YYYYMMDD (e.g.. 20151211). A list of Payment Dates can be found in the NEM settlement calendar in [S:\\Wholesale Power Trading\\Settlements]().  
Rename the two spreadsheets beginning with "_Settlements_" so that the date at the end of the filename matches the Payment Date.  
Repeat this process for every Payment Date.  
Each folder will contain 3 spreadsheets, which need to be updated in order for the invoice to be generated.

Settlements Revision Spreadsheet
--------------------------------

Open the spreadsheet named _Settlements Revision – YYYY-MM-DD_. This spreadsheet will calculate the settlement amounts for the Final Week, the 20 Week Revision and the 30 Week Revision.  
Click the "_Get Data"_ button in the "_Weekly Settlement_" sheet, to update the half hourly pool price and load data. The button is located around Cell A2.  
Save the spreadsheet.  
In the "_Weekly Settlement_" sheet, identify the appropriate NEM Week (Column B) from the **Settlement Week Finder** spreadsheet discussed in the previous [section]().

*   For the Final Week, identify the appropriate row and the amount to be invoiced is located in _Difference Payment_ (Column I).
*   For the 20 Week Revision, identify the appropriate row/rows and the amount to be invoiced is located in _CFD Adjustment_ (Column Q).
*   For the 30 Week Revision, identify the appropriate row/rows and the amount to be invoiced is located in _CFD Adjustment_ (Column V).

A positive dollar amount on the spreadsheet indicates that WPT will pay OPG.  
A negative dollar amount on the spreadsheet indicates that OPG will pay WPT.

  
If the current Payment Date includes **End of Month Adjustments** (Load Proportion, High Growth, Increased Load Premium or Reduced Load Premium), the amounts to be charged can be found in the _Mthly Settlement_ sheet. Check Cells Q15 to Q17 of the "**Settlement Week Finder**" to determine which month and which load version is applicable (Final, 20 Week Revision or 30 Week Revision).

*   For the **Final** End of Month Adjustments:
    *   Increased Load Premium is located in Column C (_Increased Load Premium (ICP))_
    *   Reduced Load Premium is located in Column D (_Reduced Load Premium (CSP)_)
    *   High Growth Adjustment is located in Column F (_High Growth Adjustment_)
    *   Load Proportion Adjustment is located in Column G (_Load Proportion Adjustment_)

*   For the **20 Week** **Revision** End of Month Adjustments:
    *   Increased Load Premium is located in Column U (_Adjustment (ICP Only))_
    *   Reduced Load Premium is located in Column V (_Adjustment (CSP Only)_)
    *   High Growth Adjustment is located in Column W (_Adjustment (__High Growth Only)_)
    *   Load Proportion Adjustment is located in Column X (_Adjustment (Load Proportion Only)_)

*   For the **30 Week Revision** End of Month Adjustments:
    *   Increased Load Premium is located in Column AJ (_Adjustment (ICP Only))_
    *   Reduced Load Premium is located in Column AK (_Adjustment (CSP Only)_)
    *   High Growth Adjustment is located in Column AL (_Adjustment (__High Growth Only)_)
    *   Load Proportion Adjustment is located in Column AM (_Adjustment (Load Proportion Only)_)

Settlements Spreadsheet
-----------------------

Open the spreadsheet named _Settlements – YYYY-MM-DD_. This spreadsheet is a cut down version of the Settlements Revision spreadsheet. It only contains the Final data and no 20 week or 30 week revision data, thus making it more suitable as an email attachment. Update this spreadsheet, save it and include it as an attachment as part of the invoice email correspondence with OPG.  
To update the half hourly pool price and load data, click the "_Get Data"_ button in the "_Weekly Settlement_" sheet. The button is located around Cell A2.  
Check that the _Difference Payment_ calculated in Column I matches the amount previously calculated using the Settlements Revision Spreadsheet, also in Column I.  
A positive dollar amount on the spreadsheet indicates that WPT will pay OPG.  
A negative dollar amount on the spreadsheet indicates that OPG will pay WPT.  
Save the spreadsheet.

Database
--------

Run the following SQL queries to double check the amounts calculated using the settlement spreadsheets.  
Connect to the MEL-SVR-DB-002 SQL database using an appropriate version of SQL Server Management Studio.  
Run the following view \[WPT\].\[OPG\_Weekly\_LFH\_CFD\_Summary\] by the following actions:

*   Click on _WPT_ =\> _Views_ =\> _dbo._ OPG\_Weekly\_LFH\_CFD\_Summary.
*   Right click and choose "_Select Top 1000 Rows"_.
*   A new window will open with some auto generated script. Append the following at the end of the auto generated script: "Order by code"
*   Rerun the query by pressing F5.

This query will produce a similar report to that found in the Settlements spreadsheet.  
Find the corresponding NEM Week under column _Code_. Highlight the row by clicking on the row number on the first column of the report, and then scroll across to find the appropriate column.

*   For the Final Week amount, use the column named _Final CFD_.
*   For the 20 Week Revision amount, use the column named _20WK CFD Adjustment_
*   For the 30 Week Revision, use the column named _30WK CFD Adjustment_

A positive amount on the database report indicates that OPG will pay WPT.  
A negative amount on the database report indicates that WPT will pay OPG.  
**NOTE**: The signage of the database report is opposite to that of the spreadsheet.  
These should be compared with the _Weekly Settlements_ tab in the _Settlements_ spreadsheet.

  
To confirm that the amounts for the monthly adjustments are also accurate, run the following view \[WPT\].\[OPG\_Mthly\_LFH\_CFD\_Summary\]

*   Click on _WPT_ =\> _Views_ =\> _dbo._ OPG\_Mthly\_LFH\_CFD\_Summary.
*   Right click and choose "_Select Top 1000 Rows"_.
*   A new window will open with some auto generated script. Append the following at the end of the auto generated script: "Order by Year, Month"
*   Rerun the query by pressing F5.

From the report generated, identify the appropriate Year and Month, then look under the following columns:

*   _Final High Growth Adjustment_
*   _20WK High Growth Adjustment_
*   _30WK High Growth Adjustment_
*   _Final Load Proportion Adjustment_
*   _20WK Load Proportion Adjustment_
*   _30WK Load Proportion Adjustment_
*   _Increased Load Premium (Final)_
*   _Reduced Load Premium (Final)_
*   _Increased Load Premium (20WK Adjustment)_
*   __Reduced_ Load Premium (_20WK Adjustment_)_
*   _Increased Load Premium (3_0WK Adjustment_)_
*   __Reduced_ Load Premium (3_0WK Adjustment_)_  
      
    

And compare these amounts with the _Monthly Settlements_ tab in the _Settlements_ spreadsheet.

Should any of the amounts not match, flag the issue and forward it to the Head of Trading Operations to investigate.

**NOTE**: The database uses a different methodology to calculate the High Growth and Load Proportion adjustments compared to the spreadsheet. Therefore, the figures might not match up individually. However, the sum of High Growth and Load Proportion adjustments on the spreadsheet should match the sum of High Growth and Load Proportion adjustments in the database.

SA & NSW Pool Cost
------------------

A final check involves checking that the final pool payment calculated in the settlement spreadsheet matches that on the AEMO invoice. Because of some OPG customers located on a South Australian Connection Point or New South Wales Connection Point, there is a slight discrepancy between the settlement spreadsheet amount and the AEMO invoice. This step is to reconcile the difference in the pool payment calculated.  
Find the AEMO Invoice from [](). The email should be received around the middle of the day and is titled "AEMO Settlements Direct: NEM Final Statement _YYYY_WK_AA_", containing a zip file attachment with the name "ONLINEPG\_PDFTAXINVOICE\_YYYYMMDD.R012.zip".  
Open this email and attachment. The attachment will ask for a password to access the page.  
**Password**: DPON0801  
Look at the section titled _Supplies Made by AEMO_, under heading _Energy GST Exclusive_. This amount will need to be compared to the _Pool Payment_ (Column J) in the Settlements spreadsheet.  
It is likely that there will be a small variance between the two. This needs to be confirmed.  
Open the spreadsheet named "SA & NSW Poolcost" where the other two settlement spreadsheets are located.  
Select the _Settlement Week_ in the dropdown list in Cell K6.  
Click the _Get Data_ button.  
This will calculate the difference between the two costs and display the variance in _Pool Cost_, cell K9. This variance will need to be included in the email that is sent off.  
Save the spreadsheet and include it as an attachment as part of the invoice email correspondence with OPG.

Invoice Generation
------------------

Login to Xero with the following details:  
Username: []()  
Password: Energy2014  
Select _Wholesale Power Trading_ from the dropdown box at the top.  
If a net amount is payable to WPT, generate an invoice. On the Xero dashboard, Under _Invoices Owed to you_ on the right, select _Draft Invoice_ or click _New Sales Invoice_ to start from the beginning.  
If a net amount is payable to OPG, generate a credit note. On the Xero dashboard, click on _Accounts_ on the top of the screen next to _Dashboard_, and select _Sales_. Next to the "+New" button, click on the downward arrow and select "_Credit note_".  
The following details need to be included on the invoice/credit note:

*   To: Online Power and Gas Pty Ltd
*   Date: this is the final statement date found on the AEMO calendar. (In the case of Credit Note, populate this field with the Payment Date)
*   Due Date: this is the Payment Date (Option not available for Credit Note)
*   Invoice #: this is automatically generated, and does not need to be altered
*   Reference: this can be left blank if not known
*   Branding: WPT
*   Description:
*   Difference payment for NEM Week X
*   20 Week Revision for NEM Week Y
*   30 Week Revision for NEM Week Z
*   High Growth Final Adjustment for MMM-YYYY (if required)
*   High Growth 20 Week Revision Adjustment for MMM-YYYY (if required)
*   High Growth 30 Week Revision Adjustment for MMM-YYYY (if required)
*   Load Proportion Final Adjustment for MMM-YYYY (if required)
*   Load Proportion 20 Week Revision Adjustment for MMM-YYYY (if required)
*   Load Proportion 30 Week Revision Adjustment for MMM-YYYY (if required)
*   Increased Load Premium for MMM-YYYY (if required)
*   Increased Load Premium 20 Week Revision for MMM-YYYY (if required)
*   Increased Load Premium 30 Week Revision for MMM-YYYY (if required)  
    
*   Reduced Load Premium for MMM-YYYY (if required)
*   Reduced Load Premium 20 Week Revision for MMM-YYYY (if required)
*   Reduced Load Premium 30 Week Revision for MMM-YYYY (if required)  
    
*   Facility Fee for Credit Support (if required)
*   Unit Price: Appropriate calculated amount. Take note of the signage depending on whether it is an invoice or credit note.
*   Account: 201- Income-Load Following Agreements
*   Tax Rate: GST Free Income
*   Counterparties: Online Power and Gas

  
Once all amounts and details have been verified, the invoice/credit note can be approved and printed as PDF. This will need to be attached with the other two documents, to be emailed to OPG's accounts department.

Email Invoice
-------------

Send the PDF invoice and the two spreadsheet attachments to: []()  
The email will need to include:

*   Subject line: "WPT Settlements NEM Week 46 (as an example)"
*   Body: "Dear OPG

Please find attached the invoice for NEM Week 49 (e.g.).  
This week's invoice includes the adjustment due to the High Growth load for November 2015 (or: This week's invoice includes the 20 Week Revision adjustments for November 2015, e.g.).  
And finally, please note that the Pool Payment on the Settlements spreadsheet differs from AEMO's invoice ($1.40) (e.g.) due to some energy that's settled on the NSW node which is not covered by the hedge agreement."

*   3 attachments: Invoice, Settlements spreadsheet, SA Poolcost

Payment
-------

If a credit note is generated, WPT needs to pay OPG (positive number in spreadsheet and negative number in database report). Put in a bank transaction to be received by OPG 1 day prior to the Payment Date if using CBA CommBiz. If using other banking platforms, schedule the transaction to be received by OPG 2 days prior to the Payment Date so that it arrives on time.

