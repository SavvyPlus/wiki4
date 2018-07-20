<!-- TITLE: Ms Sql Etl Glue -->
<!-- SUBTITLE: This is how to replicate the system and control for Glue to hadle MS SQL ON Premise connection, thisis a temp wiki as is the POC for reproduction, will need some CloudFormation for MVP and full testing for Production -->

# The Flow

![Screen Shot 2018 07 20 At 1 07 37 Pm](/uploads/screen-shot-2018-07-20-at-1-07-37-pm.png "Screen Shot 2018 07 20 At 1 07 37 Pm")


## Glue Connection Settings 
### You need to Use the AWS Glue Dashboard to create

* Add a database 
* The Move to Add connection 
 			*  Name the connection (ex. MyMSConnection )
 			*  Select JDBC as the connection type
* The URL Structure should follow 
```text
jdbc:sqlserver://MEL-SVR-DB-002:1433;databaseName=[DatabseName]
```
* Username : glue_me_please , passwoord is on the password.savvy.work pages. 
* VPC setting are
					* vpc-52292d36 | aws2_vpc_dts
					* subnet-4ef5c617 | aws2_sub_dev_priv_2c
					* sg-6a2fbd0c | aws2_sg_dev_priv
* Boila it's finish

### Now let's Crawl this baby 

* Add Crawler 
* Name the Crawler 
* Choose a data store : JDBC
* Connection : MyMSConnection (from the previous step) 
* No Exclude patterns need it for this settings 
* On Add another data store not for now, but we will add more once the POC is finished 
* IAM role Choose oscar.omegna_dev_test_glue or any other role you've created for this exercise 
* Frequency : for now we will leave it on demand , on production has to be at every change
* Set the Database where to store the catalogs 


### To be finish soon
  			
