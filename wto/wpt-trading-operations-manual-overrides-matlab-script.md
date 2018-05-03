<!-- TITLE: Wpt Trading Operations: Manual Overrides - Matlab Script -->
<!-- SUBTITLE: A quick summary of Wpt Trading Operations: Manual Overrides - Matlab Script -->



WPT Trading Operations : Manual Overrides – MATLAB Script
=========================================================



**High Growth Discount and Increased/Reduced Load Premium**
===========================================================

Line 230, 
```sql server 
if ACTUAL == 1 
```

When the actual High Growth Discount and Increased/Reduced Load Premium have been charged, the actual values can be used to override those calculated by the model to overcome inaccuracies due to the weekly resolution used.  
Connect to the MEL-SVR-DB-002 SQL database using an appropriate version of SQL Server Management Studio and run the following query. Note that the later months might not have the full complete set days with final version data available.

  



```sqlserver
SELECT Year, Month, \[Final High Growth Adjustment\], \[Increased Load Premium (Final)\], \[Reduced Load Premium (Final)\]  
FROM \[WPT\].\[dbo\].\[OPG\_Mthly\_LFH\_CFD\_Summary\]  
order by Year, Month
```



**Counterparty Initial Margin for Flat Swaps**
==============================================

Line 280, 
```sql server
if ACTUAL == 1  
```
The model assumes a default initial margin of $20,000 per MW per quarter for Q1 contracts and $8,500 per MW per quarter for all other quarters. To correct for the actual initial margin agreed upon for actual contracts, these assumed values need to be reversed out. The code from lines 280 to 340 deals with this scenario.

**Flat Swap CFD**
=================

Line 360, 
```sql server
if ACTUAL == 1
```
The model uses a weekly resolution, thus contracts that do not start on the first day of the NEM week or do not end on the last day of the NEM week will have an incorrect CFD calculated.  
The code from line 360 to 370 corrects for these inaccuracies with the actual CFD values. The actual values can be found by running the following query and using the values from the \[Flat Swap CFD\] column.

 ```sql server 
SELECT *  
FROM \[WPT\].\[dbo\].\[MBL\_Weekly\_CFD\]  
order by Code
```

**Load Following Hedge CFD**
============================

Line 450, 
```sql server
if ACTUAL == 1 
```
Similarly, due to the model's weekly resolution, the quarterly load following contracts do not always start on the first day of the NEM week or end on the last day of the NEM week. Thus inaccuracies are introduced.  
The code from line 450 to 455 corrects for these inaccuracies with the actual CFD values. The actual values can be found by running the following query and using the values from the \[Final CFD\] column.

```sql server  
SELECT *  
FROM \[WPT\].\[dbo\].\[OPG\_Weekly\_LFH\_CFD\_Summary\]  
order by Code 
```