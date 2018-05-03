<!-- TITLE: Ad Hoc Meter Data -->
<!-- SUBTITLE: A quick summary of Ad Hoc Meter Data -->


Loading Meter Data : Ad Hoc Meter Data 
=======================================


Step-by-step guide
------------------

An example template can be found here: S:\\Consulting\\Tools\\Meter Data Loading Template.xlsx

1.  Ensure that the column names match those listed in the template. These are case-sensitive.
2.  Not all columns are required, the following columns are a minimum: Timestamp,MeterRef,IntervalLength,Imp\_KVARH,Exp\_KVARH,Imp\_KWH,Exp\_KWH,TimestampType,QualityCode
3.  If only the NMI is available, use the "MeterRef" column. Otherwise, use the "NMI" and "StreamRef" columns.
4.  For TimestampType, use either "PE" Period Ending or "PS" Period Starting.
5.  For QualityCode, X = Unknown.
6.  Save the file as a CSV.
7.  Copy the file to E:\\MeterData\\Queue\\Ad-hoc on mel-svr-app-001 for the MeterDataLoader to start processing the file.

  


    

