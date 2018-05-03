<!-- TITLE: Admin Task : Tas Hydro  -->

 

Admin Task : Tas Hydro
=======================



**Every Tuesday, the database in SQL needs to be updated with the Energy Storage Levels found on the Tas Hydro website.**

  

Click onto this website, and download the latest Excel file of Energy Data

[http://www.hydro.com.au/water/energy-data](http://www.hydro.com.au/water/energy-data)

  

Open the folder found here, to save the file with the date (YYYY,MM,DD):

S:\\MarketData\\Tas Hydro\\Water Storage\\WeeklyFiles

  

Once the file has been saved, open the Master sheet found here:

S:\\MarketData\\Tas Hydro\\Water Storage\\HydroTas Energy Storage MASTER

Copy the latest row of the new file into this sheet. This will then update the next tab called "UPDATE" (check this this is choosing the corresponding date)

Open the UPDATE tab in the spreadsheet, and under the heading SQP, select all info here and Copy it. This will be pasted into the SQL database to insert the new data.

  

**SQL Management Server 2014**

New Query

Copy and Paste the column called SQL in MASTER spreadsheet

Execute

  

Open:

\[dbo\].\[TAS_HydroTasEnergyStorage\]

Right click and select Top 1000

Copy and Paste all of the info into the top section

Run

  

This will update the SQL Database with all of the new information that we have now put into the spreadsheet. You can check that this has worked by writing:


```sql
Select *

From \[dbo\].\[TAS_HydroTasEnergyStorage\]

WHERE date = (' right in the date that you just entered info for eg. '2016-05-02')
```
Run



This will show the latest info that has now been entered

  

  


