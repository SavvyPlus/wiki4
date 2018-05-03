<!-- TITLE: Loading Data -->
<!-- SUBTITLE: A quick summary of Loading Data -->

# Loading Data

## Choosing an ingestion method

Druid supports streaming (real-time) and file-based (batch) ingestion methods. The most popular configurations are:

* Files 
	* Load data from **HDFS, S3, local files, or any supported Hadoop filesystem** in batches. We recommend this method if your dataset is already in flat files.

* Stream push 
	* Push a data stream into Druid in real-time using **Tranquility**, a client library for sending streams to Druid. We recommend this method if your dataset originates in a streaming system like Kafka, Storm, Spark Streaming, or your own system.

* Stream pull 
	* Pull a data stream directly from an external data source into Druid using Realtime Nodes.

## Getting started
The easiest ways to get started with loading your own data are the three included tutorials.

* [Files](http://druid.io/docs/0.12.0/tutorials/tutorial-batch.html)
	- based tutorial showing you how to load files from your local disk.
	
* [Streams](http://druid.io/docs/0.12.0/tutorials/tutorial-streams.html)
	- based tutorial showing you how to push data over HTTP.
	
* [Kafka](http://druid.io/docs/0.12.0/tutorials/tutorial-kafka.html)
	- based tutorial showing you how to load data from Kafka.

## Hybrid batch/streaming
You can combine batch and streaming methods in a hybrid batch/streaming architecture. In a hybrid architecture, you use a streaming method to do initial ingestion, and then periodically re-ingest older data in batch mode (typically every few hours, or nightly). When Druid re-ingests data for a time range, the new data automatically replaces the data from the earlier ingestion.

_All streaming ingestion methods currently supported by Druid do introduce the possibility of dropped or duplicated messages in certain failure scenarios, and batch re-ingestion eliminates this potential source of error for historical data._

Batch re-ingestion also gives you the option to re-ingest your data if you needed to revise it for any reason.