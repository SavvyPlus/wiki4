---
title: New Loaders
description: New Loaders are serverles  applications deployed on AWS cloud for the purpose of processing source files and ingesting the data into Sql Server
published: true
date: 2019-12-17T03:38:25.671Z
tags: 
---

# Loaders

The loader or "hanlders" are norrow purpose lambda build that allows to recieve and process different data sources into DB and tables hosted in S3 and query by Athena, this is where we prepare the first source data to be anaylses and manipulated accordanly 

## ETL 
Our loaders are store in github and each one of the has an explanation and README file to expalin theri structure and function, they difference from other as they all in the format **etl**-handler-name 



# Downloaders
Downloader are what we use to bring the data to S3 from different sources , each downloader naming should be as follow **dl**-name-desc. 

## Feeding 
The Dowloader feed into the input folders for the Loaders, the concept of download is to "Download from a website" to S3, while this may not make traditional logical sense , in the begining the files were downloaded to a Server and then loaded to SQL since we kept the name to ease the transition


# Scrappers
Scrappers may or may not be supported by downloaders, as the web has great information the scrappers allows to collect in from information center that dont provide data tranfer protocols , or for fast news and movement that are not really reported in formal settings. 

