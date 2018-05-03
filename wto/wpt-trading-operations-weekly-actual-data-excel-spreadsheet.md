<!-- TITLE: WPT Trading Operations: Weekly Actual Data Excel Spreadsheet -->
<!-- SUBTITLE: A quick summary of WPT Trading Operations: Weekly Actual Data Excel Spreadsheet -->


WPT Trading Operations : Weekly Actual Data – Excel Spreadsheet
===============================================================


If actual data is to be used in the cash forecast run, the "Wkly Actuals" sheet of the spreadsheet needs to be updated with the most recent data. This can be done by running the view \[WPT\].\[dbo\].\[WPT\_Weekly\_Actuals\].  
Connect to the MEL-SVR-DB-002 SQL database using an appropriate version of SQL Server Management Studio and run the following query:



```sqlserver
SELECT *  
FROM \[WPT\].\[dbo\].\[WPT\_Weekly\_Actuals\]  
order by Code
```


  
Update the data in Columns F to J in the spreadsheet, starting from row 8.