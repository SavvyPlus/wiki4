---
title: New Loaders
description: New Loaders are serverles  applications deployed on AWS cloud for the purpose of processing source files and ingesting the data into Sql Server
published: true
date: 2019-12-17T04:07:32.054Z
tags: 
---

# MarketData Downloader and SavvyLoaders
This application is built to download or scrape files related to the energy market from the Internet. Then, this tool processes the files and ingests the market data into the Sql Server.
## MarketData Downloader
Github link: https://github.com/SavvyPlus/market-data-downloader-cf/tree/dex_cfn_empower



## MarketDispatch
1
2
3
4
5
123

123

123

123
213
12
321
312
3213
123
12
312
3
123
12
3
213
21
3
123
21






## Savvyloader


# Invoice Loader
Github link: 
The invoice loader querys the InvoiceLoader.dbo.InvoiceLoaderJobs first to get the job defination.
## Upload Instruction
1. Prepare the invoice csv files
2. Log in to the AWS account(SavvyPlus).  Open the s3 bucket invoice-loader-prod-invoice-loader-savvyplus and then open the  in folder
3. Inside the in folder,  upload invoice files to appropriate folder with proper EDI_format and organisation_identifier(create it if necessary)
4. Wait for a few seconds, if successful, the files will be moved to the done folder in the bucket; if not, the files will be moved to the error folder, in this case, please contact Dex or Anh.


# Meter Loader




