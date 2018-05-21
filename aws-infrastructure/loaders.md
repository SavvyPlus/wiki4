<!-- TITLE: Savvy Loaders and Downloaders-->
<!-- SUBTITLE: We use loader, downloader and sometimes scrappers to collect data and make it part of our resources to deliver sweet as visualisations  -->

![Dl Sc Ld](/uploads/dl-sc-ld.png "Dl Sc Ld")

# Loaders

The loader or "hanlders" are norrow purpose lambda build that allows to recieve and process different data sources into DB and tables hosted in S3 and query by Athena, this is where we prepare the first source data to be anaylses and manipulated accordanly 

## ETL 
Our loaders are store in github and each one of the has an explanation and README file to expalin theri structure and function, they difference from other as they all in the format **etl**-handler-name 

### Folders 
In our Buckets each forlder reperesents a table , which is what we query using Athena. We recently moved from bucket processing to folder processing each output folder is then move to the warehouse using other services such as Glue and Lambda

# Downloaders
Downloader are what we use to bring the data to S3 from different sources , each downloader naming should be as follow **dl**-name-desc. 

## Feeding 
The Dowloader feed into the input folders for the Loaders, the concept of download is to "Download from a website" to S3, while this may not make traditional logical sense , in the begining the files were downloaded to a Server and then loaded to SQL since we kept the name to ease the transition


# Scrappers
Scrappers may or may not be supported by downloaders, as the web has great information the scrappers allows to collect in from information center that dont provide data tranfer protocols , or for fast news and movement that are not really reported in formal settings. 

