<!-- TITLE: Clustering -->
<!-- SUBTITLE: A quick summary of Clustering -->

# Clustering

**Druid is designed to be deployed as a scalable, fault-tolerant cluster.**

In this document, we'll set up a simple cluster and discuss how it can be further configured to meet your needs. This simple cluster will feature scalable, fault-tolerant servers for Historicals and MiddleManagers, and a single coordination server to host the Coordinator and Overlord processes. In production, we recommend deploying Coordinators and Overlords in a fault-tolerant configuration as well.

## Select hardware

The Coordinator and Overlord processes can be co-located on a single server that is responsible for handling the metadata and coordination needs of your cluster. The equivalent of an AWS m3.xlarge is sufficient for most clusters. This hardware offers:
	* 4 vCPUs
	* 15 GB RAM
	* 80 GB SSD storage
<br>

Historicals and MiddleManagers can be colocated on a single server to handle the actual data in your cluster. These servers benefit greatly from CPU, RAM, and SSDs. The equivalent of an AWS r3.2xlarge is a good starting point. This hardware offers:
	* 8 vCPUs
	* 61 GB RAM
	* 160 GB SSD storage

<br>

Druid Brokers accept queries and farm them out to the rest of the cluster. They also optionally maintain an in-memory query cache. These servers benefit greatly from CPU and RAM, and can also be deployed on the equivalent of an AWS r3.2xlarge. This hardware offers:
	* 8 vCPUs
	* 61 GB RAM
	* 160 GB SSD storage
<br>

You can consider co-locating any open source UIs or query libraries on the same server that the Broker is running on. Very large clusters should consider selecting larger servers.

## Select OS
We recommend running your favorite Linux distribution. You will also need: _Java 8 or better_

Your OS package manager should be able to help for both Java. If your Ubuntu-based OS does not have a recent enough version of Java, WebUpd8 offers packages for those OSes.

## Download the distribution
First, download and unpack the release archive. It's best to do this on a single machine at first, since you will be editing the configurations and then copying the modified distribution out to all of your servers.
```
curl -O http://static.druid.io/artifacts/releases/druid-0.12.0-bin.tar.gz
tar -xzf druid-0.12.0-bin.tar.gz
cd druid-0.12.0
```
<br>

In this package, you'll find:

`LICENSE` - the license files.
`bin/` - scripts related to the single-machine quickstart.
`conf/*` - template configurations for a clustered setup.
`conf-quickstart/*` - configurations for the single-machine quickstart.
`extensions/*` - all Druid extensions.
`hadoop-dependencies/*` - Druid Hadoop dependencies.
`lib/*` - all included software packages for core Druid.
`quickstart/*` - files related to the single-machine quickstart.

We'll be editing the files in `conf/` in order to get things running.

## Configure deep storage

Druid relies on a distributed filesystem or large object (blob) store for data storage. The most commonly used deep storage implementations are **S3 (popular for those on AWS)** and HDFS (popular if you already have a Hadoop deployment).

### S3

In `conf/druid/_common/common.runtime.properties`:

* Set druid.extensions.loadList=["druid-s3-extensions"].

* Comment out the configurations for local storage under "Deep Storage" and "Indexing service logs".

* Uncomment and configure appropriate values in the "For S3" sections of "Deep Storage" and "Indexing service logs".

After this, you should have made the following changes:
```
druid.extensions.loadList=["druid-s3-extensions"]

#druid.storage.type=local
#druid.storage.storageDirectory=var/druid/segments

druid.storage.type=s3
druid.storage.bucket=your-bucket
druid.storage.baseKey=druid/segments
druid.s3.accessKey=...
druid.s3.secretKey=...

#druid.indexer.logs.type=file
#druid.indexer.logs.directory=var/druid/indexing-logs

druid.indexer.logs.type=s3
druid.indexer.logs.s3Bucket=your-bucket
druid.indexer.logs.s3Prefix=druid/indexing-logs
```