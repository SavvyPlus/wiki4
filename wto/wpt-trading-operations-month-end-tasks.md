<!-- TITLE: WPT Trading Operations: Month End Tasks -->
<!-- SUBTITLE: A quick summary of WPT Trading Operations: Month End Tasks -->

Mark-to-Market
==============

For accounting purposes, it is necessary to perform mark to market to provide a realistic valuation of WPT's contracts on a regular basis. This requires updating two spreadsheets, one to value the load following hedge with OPG, and one to value the OTC contracts with Macquarie Bank.  
The spreadsheets can be found here: [S:\\Wholesale Power Trading\\Mark to Market]()

Load Following Hedge
--------------------

The name of the mark to market spreadsheet for the load following hedge begins with "_LFH MtM – YYYYMMDD_".  
Make a copy of the latest spreadsheet and rename the date field to be the date at which the contracts are being valued (i.e. Does not have to be the same date as when the mark to market is being run).  
Open the spreadsheet.  
On the "_Weekly Settlement_" sheet, update the "_As at Date_" field in Cell Q3. This is the date as which the contracts are being valued.  
On the "_Weekly Settlement_" sheet, update the "_Load Forecast ID_" field in Cell Q4 as required. The following database table in the MEL-SVR-DB-002 server contains a list of all Load Forecast ID.

*   \[WPT\].\[dbo\].\[Load\_Forecast\_Header\]

Click the "_Get Data"_ button in the "_Weekly Settlement_" sheet. This will update the half hourly pool price and load data, and retrieve the Futures contract settlement prices that correspond to the "As at Date". The button is located around Cell A1.  
The mark to market results can be found in the "_Mthly Settlement_" sheet.  
Save the spreadsheet.

OTC Contracts
-------------

The name of the mark to market spreadsheet for the OTC contracts begins with "M_tM Template v8 – YYYYMMDD_".  
Make a copy of the latest spreadsheet and rename the date field to be the date at which the contracts are being valued (i.e. Does not have to be the same date as when the mark to market is being run).  
Open the spreadsheet.  
On the "_Inputs_" sheet, update the "_As at Date_" field in Cell J24. This is the date as which the contracts are being valued.  
On the "_Inputs_" sheet, update the "_Load Forecast ID_" field in Cell J25 as required. The following database table in the MEL-SVR-DB-002 server contains a list of all Load Forecast ID.

*   \[WPT\].\[dbo\].\[Load\_Forecast\_Header\]

Click the "_Get Data"_ button in the "_Inputs_" sheet. The button is located around Cell L24. This will update the half hourly pool price and load data, and retrieve the Futures contract settlement prices that correspond to the "As at Date". The list of OTC contracts in the "_Contracts_" sheet is also updated.  
Check the "HH Calcs" sheet to ensure that all contracts have been included in the mark to market calculations. If contracts are missing, perform the following steps:

*   Drag the existing formula in rows 1 to 11 from the last available column across to the next free column.
*   Remove the array formula braces {} from the new formula in row 11.
*   Populate rows 12 to 50410 of the new column with "1"s.
*   Select rows 11 to 50410 of the new column and apply the array formula by pressing Ctrl, Shift and Enter.
*   Repeat the above steps for each missing contract.

Check the _Mthly MtM Settled_" and "_Mthly MtM Not Settled_" sheets that all contracts have been included in the mark to market calculations. If contracts are missing, drag the existing formula in rows 1 to 46 from the last available column across to the next free column until all contracts are included. There are no array formulas so this is the only action required.  
Check the "_Weekly MtM_" sheets that all contracts have been included in the mark to market calculations. If contracts are missing, drag the existing formula in rows 1 to 173 from the last available column across to the next free column until all contracts are included. There are no array formulas so this is the only action required.  
The mark to market results can be found in the "_Key MTM Figures_" sheet. Check that the formulas in Columns B, C and H has extended long enough (in the column references) to include all new contracts in the _Mthly MtM Settled_" and "_Mthly MtM Not Settled_" sheets. Update the formulas as required.  
Save the spreadsheet.

Monthly Forecast Prices
=======================

WPT is obligated to send OPG indicative prices for each quarter for the remainder of the term of the agreement. This must be done within 5 business days of the start of each month.  
Open the following spreadsheet:  
[S:\\Wholesale Power Trading\\Online Power & Gas\\2016\\Monthly Prices](file:////savvyplus.local//CompanyData//Wholesale Power Trading//Online Power & Gas//2016//Monthly Prices) with the most recent date. Make a copy of this file, and save with the latest date (eg. 20151231)  
The aim is to update the numbers in the _Settlement Prices_ tab. To do this, open the following:  
C:\\Dev\\Python Functions\\OPG Price Template or it can be found in the **Code Repository**  
Under the _Input Variable_ comment, change the _StartDate_ variable to be the last day of the previous month.  
Run this script by pressing F5 and then open the spreadsheet created by the script: [C:\\Development\\OPG Indicative Price Template.xlsx]()  
Copy all of the prices and dates in the script, and paste it into the Monthly Prices spreadsheet. This might have to be done separately as dates, then prices so that all of the numbers correspond with the correct quarters.  
Within the spreadsheet, open the tab _Price Schedule (Base Energy)_ and change the date in the top right hand side. This will also need to be done for all 3 tabs.

Loan Interest Payments
======================

WPT has loan agreements with a number of entities. The interest for these loans are paid either monthly, quarterly or annually, within 7 days of the end of the period. To determine the loan interest to be paid,

*   Open the folder:

[S:\\Wholesale Power Trading\\Weekly Cash Forecasts]() and select the latest _Cashflow Model_ spreadsheet.

*   Click on the _Loans_ sheet, and find the appropriate week to show the amounts for the different entities. For example, interest due for the month November 2015 can be found in Row 50, payable within 7 days of 30 November 2015 and interest due for the month December 2015 can be found in Row 54, payable within 7 days of 31 December 2015
*   For each entity which has an interest amount due, create the appropriate transaction in CBA CommBiz and make the amount payable within 7 days of the end of the calendar month.

  
Here are the banking details for each entity:

  
**Daley Family Trust**  
BSB: 063-840  
Account: 1014 6818

  
**Regina Pacis Investment Pty Ltd**  
BSB: 033-053  
Account: 649517

  
**Tobias Geiger**  
BSB: 123-637  
Account: 22334663

  
**Online Power and Gas Pty Ltd**  
BSB: 063-162  
Account: 10557414

  
**Saikrishna** **Thota**  
BSB: 013-013  
Account: 507186895

  
**Ninety-Sixth Lieutenant Pty Ltd**  
BSB: 063-113  
Account: 10487545

