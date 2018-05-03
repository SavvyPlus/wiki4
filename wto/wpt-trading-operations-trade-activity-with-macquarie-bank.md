<!-- TITLE: WPT Trading Operations: Trade Activity With Macquarie Bank -->
<!-- SUBTITLE: A quick summary of WPT Trading Operations: Trade Activity With Macquarie Bank -->


Summary Email
=============

For each trade with WPT, an email will be sent from Macquarie Bank to WPT's Trading Manager, detailing information about the deal. This will include important dates and costings, along with a PDF of the actual contract.

Trade log
=========

All trades entered into by WPT are recorded in the trade log.  
The trade log can be found here: [S:\\Wholesale Power Trading\\CTS Reports\\Trade Activity Log.xlsx]()  
Key information to record include:

*   Contract start date
*   Contract end date
*   Trade date
*   Trade details (derivative type, price, quantity, region, exchange)
*   Trader's name
*   Authorising person
*   Counterparty
*   Confirmation date
*   Back office person confirming
*   Initial margin
*   Supporting documentation

  
In addition, settlement calculation spreadsheets will have to be updated to include new contract prices and volume, these can be found here: [S:\\Wholesale Power Trading\\Settlements]() (See Settlements Section for more details)

Contracts Register
==================

  
All contracts entered into with WPT need to be recorded in the Contracts Register.  
The Contracts Register can be found here: [S:\\Wholesale Power Trading\\Trades\\Contract Register.xlsx]()  
Key information to record include:

*   Contract Type
*   Reference (if available)
*   Description
*   State Date
*   End Date
*   Contract Value
*   Counterparty
*   Contract Date
*   Additional Information (if applicable)

Database
========

The following database table in the MEL-SVR-DB-002 server will also be updated with the new contract details.

*   \[WPT\].\[dbo\].\[Contract\]

Cashflow Forecast Spreadsheets
==============================

Each trade made with WPT needs to be updated in the corresponding Weekly Cash Forecast spreadsheet. These can be found here: [S:\\Wholesale Power Trading\\Weekly Cash Forecasts]() and are updated on a weekly basis.  
Look for title _Cashflow Model_ _XYZ_.xlsx and locate the most recently dated spreadsheet. Create a copy of this spreadsheet and rename it so that it is dated for the following week's run.  
Open the spreadsheet, click on the _Actual Contracts_ tab. This following columns will need to be updated to include the new contract details:

*   Start Date
*   End Date
*   Trade Date
*   Product
*   Price
*   Volume (MW)
*   OTC

Cashflow Forecast MATLAB Script
===============================

The MATLAB script used to run the cashflow forecast will need to be updated to reflect the actual collateral exchanged with Macquarie Bank. This script can be found in  
C:\\Dev\\MATLAB Scripts\\Cashflow\_X\_Y.m or it can be found in the **Code Repository.**  
In the code, around lines 280 to 320, there is a line of code that reads "if ACTUAL ==1". Following the example of the lines of code below this, update the _WklyOTCMargin_ variable so that the automatically calculated initial margin is replaced with the actual amount exchanged.
