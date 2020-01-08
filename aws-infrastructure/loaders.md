---
title: New Loaders
description: New Loaders are serverles  applications deployed on AWS cloud for the purpose of processing source files and ingesting the data into Sql Server
published: true
date: 2020-01-08T02:33:52.571Z
tags: 
---

# MarketData Downloader and SavvyLoaders
This application is built to download or scrape files related to the energy market from the Internet. Then, this tool processes the files and ingests the market data into the Sql Server. It consists of three parts: MarketData Downloader, MarketData Dispatcher, and Savvyloader.
Asana Link: https://app.asana.com/0/751809352411794/1133019331538058
Mantenance Log: https://app.asana.com/0/751809352411794/1144804739969025
Project report: https://docs.google.com/document/d/1zIvWzR5XZP5LdMYcC5nhi1MFoaRZSpBNbitE00CXVAA/edit#
## MarketData Downloader
Github link: https://github.com/SavvyPlus/market-data-downloader-cf/tree/dex_cfn_empower
The stack of MarketData Downloader is deployed on the Empower AWS account.
The MarketData Downloader reads its job in a dynamodb **prod-marketdata_downloader_source.empower**. The files are downloaded to the s3 bucket **marketdata-downloader-prod**
## MarketData Dispatcher
Github link: https://github.com/SavvyPlus/downloader2handler-cf/tree/dex_cfn_empower2savvyplus
The stack of MarketData Downloader is deployed on the Empower AWS account.
The dispatcher automatically copies the data from **marketdata-downloader-prod** to proper s3 bucket in Empower account. It reads the mapping form a dynamodb table **table-test-downloader-handler-empower** in Empower AWS Account


## Savvyloader
The Savvyloader consists of four separate loaders: [ASX loader](https://github.com/SavvyPlus/etl-asx/tree/dex_cfn_savvyplus), [Tashydro loader](https://github.com/SavvyPlus/etl-tas-hydro/tree/dex_cfn_savvyplus), [Mecari loader](https://github.com/SavvyPlus/etl-mercari/tree/dex_cfn_savvyplus) and [CSV loader](https://github.com/SavvyPlus/etl-generic-csv). Details can be found in the [project report](https://docs.google.com/document/d/1zIvWzR5XZP5LdMYcC5nhi1MFoaRZSpBNbitE00CXVAA/edit#)


# Invoice Loader
Github link: https://github.com/SavvyPlus/etl-invoice-loader/tree/dex_cfn_savvyplus
The invoice loader querys the InvoiceLoader.dbo.InvoiceLoaderJobs first to get the job defination. And it has a threshold `MAX_CHUNK_LENGTH`, if the `RAW_EDI_MAX_LENGTH` is bigger than 6000 lines(changeable), it will split the inovice into separate invoices files.
## Upload Instruction
1. Prepare the invoice csv files
2. Log in to the AWS account(SavvyPlus).  Open the s3 bucket **invoice-loader-prod-invoice-loader-savvyplus** and then open the  **in** folder
3. Inside the in folder,  upload invoice files to appropriate folder with proper EDI_format and organisation_identifier(create it if necessary)
4. Wait for a few seconds, if successful, the files will be moved to the done folder in the bucket; if not, the files will be moved to the error folder, in this case, please contact Dex or Anh.


# Meter Loader

# NEMDE Loader
Github link: https://github.com/SavvyPlus/nemde-loader
The Nemde Loader is a script that needs to run on a machine. 

## Purpose
To better understand how the 5min spot price (wholesale cost of energy) is derived we want see which generators were responsible for setting the price. Accessing the PriceSetter files published from AEMO will help us determine this.
## Background 
AEMO currently publishes the NEMDE files (Price Setter & SPD Outputs) after the month has ended, with the data itself broken into 288 files per day (5min resolution). However, as part of our new subscription with AEMO we will be aiming to receive the data overnight going forward. The monthly files we current have downloaded are zipped and includes zipped daily files with 288x5min files inside (i.e. Whole File Zip -> Daily Zips -> 5min files). The files themselves are XML with an example attached.

## Instruction
1. Uplaod original files to s3 bucket aemo.nemde. Don't need this step if the files are up there already.
2. Put the name of the targeted zipped file into filename.txt (text files must end with a newline)
3. Run the run.sh as sh run.sh filename.txt
## Note
If the data needs to be partitioned by minutes:

The date/time of the file and naming conventions are a little misleading so please note the following. Within each daily zip there is a file for every 5min period of that day (i.e. 288 files). Each of these files has the following naming convention:

NEMPriceSetter_YYYYMMDDXXX00.xml where XXX is the 5min period number (001 = first 5min period...288 = last 5min period)

However, a day is not 00:00 to 24:00 but rather 04:05 to 04:05. Therefore, the first 5min period (001) actually refers to the period 04:00-04:05. As a result, whilst the filename states the data is for one date the data can actually span to the following day for certain 5min periods (e.g. 5min ID 240 onwwards actually has data for the following day). The attached image shows which 5min periods will have data for the day and which refer to the same day.

-> Simple Example (14th 5min period): - NEMPriceSetter_2018010101400 -> 01-Jan-2018 05:10 (i.e. 05:05-05:10)

-> Advanced Example (272nd 5min period): - NEMPriceSetter_2018010127200 -> 02-Jan-2018 02:40 (i.e. 02:35-02:40)

Why this is relevant? Partitioning the data will be done on the filename but the actual reporting of the data will be done on the partition strcuture AND the actual data/time field within the XML file itself. We will need the flexibility to report on the Year, Month, Day, Hour, Minute of the actual data as well as the partitioned filename structure.




