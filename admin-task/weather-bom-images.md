<!-- TITLE: Admin Task: Weather - BOM Images  -->


Admin Task : Weather - BOM Images
==================================

At the beginning of every month, do the following:

  

1.  Open the file  
    S:\\MarketData\\Weather Data\\BOM Climate Summary
2.  In _Setup_, type in the start date of the new month that you want to download (ie. 1-Mar-17)
3.  Click "Run Monthly"
4.  Check that all of the URLs were downloaded into _Output_
5.  Scan through columns, K, L and M to see if there are any files that didn't work (ie. 'URL not found'). These will need to be excluded when you copy the SQL statements.
6.  Copy the list of SQL statements and paste them into _New Query_ in SQL.
7.  Check on the Weather PBI report that they have updated (Production\\Weather Report).

<br>
	
1.  Open the file  
    S:\\MarketData\\Weather Data\\BOM Climate Outlook
2.  Go to the link:
    [http://www.bom.gov.au/jsp/sco/archive/index.jsp?map=rain&outlook=median&area=national&period=season1&year=2017&month=3&day=23](http://www.bom.gov.au/jsp/sco/archive/index.jsp?map=rain&outlook=median&area=national&period=season1&year=2017&month=3&day=23)
    Look for the date that is listed here in the dropdown boxes (ie. 30 Mar 2017 or for Feb, 23 Feb 2017)
    
3.  Type this date into the left hand side of the spreadsheet
4.  Click _Run_
5.  Check the column _Result_ to ensure they are all True (if there are any Falses, filter these out so that you don't enter them into SQL)
6.  Copy the SQL columns and paste into _New Query_ in SQL
7.  Check the Weather PBI report that they are there

  

Seasonal:

Repeat the steps above at the end of a season

  

Wet Season (NT)

Repeat the steps above at the start of May




