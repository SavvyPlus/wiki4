---
title: New Loaders
description: New Loaders are serverles  applications deployed on AWS cloud for the purpose of processing source files and ingesting the data into Sql Server
published: true
date: 2019-12-27T10:01:32.777Z
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
The invoice loader querys the InvoiceLoader.dbo.InvoiceLoaderJobs first to get the job defination.
## Upload Instruction
1. Prepare the invoice csv files
2. Log in to the AWS account(SavvyPlus).  Open the s3 bucket **invoice-loader-prod-invoice-loader-savvyplus** and then open the  in folder
3. Inside the in folder,  upload invoice files to appropriate folder with proper EDI_format and organisation_identifier(create it if necessary)
4. Wait for a few seconds, if successful, the files will be moved to the done folder in the bucket; if not, the files will be moved to the error folder, in this case, please contact Dex or Anh.


# Meter Loader




