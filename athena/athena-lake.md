<!-- TITLE: Athena Lake -->
<!-- SUBTITLE: Athena lake is the first stage of bucket that we query  -->

## asx_closing_history 

Previous;ly handle by SavvyLoader (legacy) 
Now a one off upload to athena due to update to the formats 

### **Where to find it now ?**

**Files **
https://s3.console.aws.amazon.com/s3/buckets/asx-closing-snapshot.history/?region=ap-southeast-2&tab=overview


**Data **

"asx_closing_snapshot_history"."closing_snapshot_futures"
"asx_closing_snapshot_history"."closing_snapshot_options"


**Handler **
NEW
https://github.com/SavvyPlus/etl-asx/tree/master/asx-final-snapshot


## asx_open-history_history 

Previous;ly handle by SavvyLoader (legacy) 
Now a one off upload to athena due to update to the formats 

### **Where to find it now ?**

**Files **
https://s3.console.aws.amazon.com/s3/buckets/asx-open-interest.history/?region=ap-southeast-2&tab=overview


**Data **

SELECT * FROM "asx_open_interest_history"."open_interest_caps" limit 10;
SELECT * FROM "asx_open_interest_history"."open_interest_futures" limit 10;
SELECT * FROM "asx_open_interest_history"."open_interest_options" limit 10;


**Handler **
NEW
https://github.com/SavvyPlus/etl-asx/tree/master/asx-open-interest-report



## asx_settlement_history 

Previous;ly handle by SavvyLoader (legacy) 
Now a one off upload to athena due to update to the formats 

### **Where to find it now ?**

**Files **
https://s3.console.aws.amazon.com/s3/buckets/asx-settlement.history/?region=ap-southeast-2&tab=overview


**Data **

SELECT * FROM "asx_settlement_history"."settlement_futures" limit 10;
SELECT * FROM "asx_settlement_history"."settlement_caps" limit 10;



**Handler **
NEW
https://github.com/SavvyPlus/etl-asx/tree/master/asx-open-interest-report




