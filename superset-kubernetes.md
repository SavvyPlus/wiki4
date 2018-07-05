<!-- TITLE: Superset Kubernetes -->
<!-- SUBTITLE: A quick summary of Superset Kubernetes -->

# Superset on Kubernetes
Savvy will use Superset [https://github.com/apache/incubator-superset] to create a business intelligence dashboard for viewing the reports that are currently available in PowerBI.

## Deployment Platform
We will deploy Superset on Kubernetes [https://kubernetes.io/] so that we can autoscale the nodes that Superset runs on to support multiple users/businesses.

### Kubernetes on AWS
![K8s](/uploads/untitled-diagram.png "K8s") 
Kubernetes is a container orchestration platform that will automatically move docker containers from a container host that is failing to a new host or can spin up a new instance of a container in a new host.

## Pre-requisites
Superset itself doesn't require any pre-requisite software, we are using druid [http://druid.io/] as a distributed data store and druid does require further software.
* Apache Zookeeper [https://zookeeper.apache.org/]
* Postgresql

## Druid configuration
Druid is made of multiple components:
* Deep storage (HDFS/S3 etc)
* Historical nodes that cache chunks of data (known as segmets) from deep storage and allow queries to be executed against them
* Broker nodes are responsible for allowing clients to connect to the druid cluster and to send queries
* Coordinator nodes are responsibel for telling the historical nodes which segments to fetch from deep storage and when to move segments across nodes

A complete description of the druid architecture can be found here [http://static.druid.io/docs/druid.pdf]

## Savvy Superset
The superset kubernetes cluster configuration code is stored here [https://github.com/SavvyPlus/superset]

This project contains the docker image `Dockerfile`s and the Kubernetes deployment/service and statefulset descriptors.

## Kops
To make managing and maintaining the kubernetes cluster easier, we are using KOps [https://github.com/kubernetes/kops]. This allows us to create and modify the kubernetes cluster without having to manually create resources in AWS (EC2 instances etc).

To make using kops easier, a docker container is available in the superset repository [https://github.com/SavvyPlus/superset/blob/master/k8s/Dockerfile] which uses kops to configure various aws resources and create a basic kubernetes cluster.

## Creating a superset kubernetes cluster
Checkout the repo from [https://github.com/SavvyPlus/superset] and:
1. `cd superset/k8s`
1. `./cluster.sh`
1. `sudo docker run -it savvybi/superset-cluster-kops:0.1`
1. From inside the superset-cluster-kops docker container, run the following to create the k8s spec
`kops create cluster --node-size=t2.large --zones=ap-southeast-2a,ap-southeast-2b --node-count=4 --name=${NAME}`
1. From inside the superset-cluster-kops docker container, run the following to use the spec to create the k8s cluster
`kops update cluster ${NAME} --yes`
1. From inside the superset-cluster-kops docker container, run the following to generate the kubectl config:
`kops export kubecfg --name=${NAME}`
1. From inside the superset-cluster-kops docker container, run the following to validate that the cluster is ready:
`kops validate cluster`