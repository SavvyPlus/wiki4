<!-- TITLE: Admin Task: LGC and STC Updates   -->


Admin Task : LGC and STC Updates
=================================

Created by Kate Daley, last modified by James Cheong on Aug 22, 2017

Once a week (preferably at the start of the week), the database in SQL needs to be updated with the information found on the Mercari Twitter feed.

Open the following database:

1.  Open SQL Server 2014 Management Studio
2.  Dble click on "Market Data"
3.  "Tables"
4.  Open dbo.Enviro_ForwardCurve
5.  Right click "Select top 1000 rows"
6.  Type "Order by Date desc" at the end of the query and rerun to find out when the data was last updated.
7.  Go to the the Mercari website on twitter and open the spreadsheet template.
8.  Enter the data from the Mercari website into the spreadsheet template, in particular, update the cells highlighted pale yellow (Columns A, C, D, F & G).
9.  Create a new SQL query and copy columns H & I of the spreadsheet into the query edit and execute the query.

  

Website: [https://twitter.com/mercarirates](https://twitter.com/mercarirates)

**Note: If entering manually into the DB, add 1 to the date of the Twitter feed as this date seems to be behind AEST by 24hr**

The spreadsheet template can be found in **S:\\MarketData\\LGCs & STCs\\Environmental Certificate Insertion Template.xlsx**

  

NOTE: Data from Mecari starting 16-Sept-2013 have been modified so that the "Date" is now +1 from what was originally in the database.

