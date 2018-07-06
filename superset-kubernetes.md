<!-- TITLE: Superset Kubernetes -->
<!-- SUBTITLE: A quick summary of Superset Kubernetes -->

# Superset on Kubernetes
Savvy will use Superset [https://github.com/apache/incubator-superset] to create a business intelligence dashboard for viewing the reports that are currently available in PowerBI.

## Deployment Platform
We will deploy Superset on Kubernetes [https://kubernetes.io/] so that we can autoscale the nodes that Superset runs on to support multiple users/businesses.

### Kubernetes on AWS
![K8s](/uploads/untitled-diagram.png "K8s") 
Kubernetes is a container orchestration platform that will automatically move docker containers from a container host that is failing to a new host or can spin up a new instance of a container in a new host.

To run Kubernetes on AWS we need to have some EC2 instances that will act as Kubernetes hosts.  These EC2 instances will all form part of the Kubernetes cluster and will run the various pods, services, deployments and statefulsets.

### Kubernetes Concepts
At it's most basic level, Kubernetes runs applications packaged as docker containers.  The key concept is that the application developer writes the application and defines the dependencies required, including memory, cpu and networking requirements.  These are packaged up as a docker container, then the deployment process involves creating a manifest yaml file which contains a reference to the newly created docker container along with instructions on how to access the container (networking ports etc) and how the container interacts with other containers.

#### Pods
Kubernetes Pods are an application container (the developer's application), along with a secondary management container that allows the cluster to manage networking and control the application container.

#### Services
Kubernetes Services are a mechanism to expose Pods outside the cluster.

#### Deployment
A Kubernetes Deployment is the description of how many instances of the Pod should be started and how they should be distributed over the nodes in the cluster.  The Deployment will check on the health of the pod and restart it if needed.

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

## KOps
To make managing and maintaining the kubernetes cluster easier, we are using KOps [https://github.com/kubernetes/kops]. This allows us to create and modify the kubernetes cluster without having to manually create resources in AWS (EC2 instances etc).

To make using kops easier, a docker container is available in the superset repository [https://github.com/SavvyPlus/superset/blob/master/k8s/Dockerfile] which uses kops to configure various aws resources and create a basic kubernetes cluster.

## Kubectl
Although `kops` is used to manage the infrastructure that the cluster runs on (in our case AWS), `kubectl` is the tool that is used to interact with the cluster, to perform the deployments of applications and to inspect the state of the applications and cluster.
## Creating a superset kubernetes cluster
Checkout the repo from [https://github.com/SavvyPlus/superset] and:
* `cd superset/k8s`
* `./cluster.sh`
* `sudo docker run -it savvybi/superset-cluster-kops:0.1`
* From inside the superset-cluster-kops docker container, run the following to create the k8s spec
`kops create cluster --node-size=t2.large --zones=ap-southeast-2a,ap-southeast-2b --node-count=4 --name=${NAME}`
* From inside the superset-cluster-kops docker container, run the following to use the spec to create the k8s cluster
`kops update cluster ${NAME} --yes`
* From inside the superset-cluster-kops docker container, run the following to generate the kubectl config:
`kops export kubecfg --name=${NAME}`
* From inside the superset-cluster-kops docker container, run the following to validate that the cluster is ready:
`kops validate cluster`

## Request SSL Certificate from AWS Certificate Manager
To allow us to use secure connections to superset running on kubernetes, we need to get an SSL certificate.  The most efficient way of doing this when working with AWS is to use AWS Certificate Manager.

* Using the AWS web console, go to Certificate Manager and request a certificate for `*.superset.savvybi.enterprises`
* Use the DNS validation method.  
* When the certificate has been validated, copy the arn of the certificate to use in the nginx.yaml and superset.yaml deployment files

## Deploying Kubernetes Dashboard

From the top level of the git repository:
* `sudo docker run -it savvybi/superset-cluster-kops:0.1`
* `kops export kubecfg --name=${NAME}`
* From inside the superset-cluster-kops docker container, run the following to deploy the kubernetes dashboard:
* `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml`
* `kops get secrets kube --type secret -oplaintext`
* Copy the output from this and use it as the password for (username admin): https://api.superset.savvybi.enterprises/ui
* `kops get secrets admin --type secret -oplaintext`
* Copy the output from this and use it as the Token

## Deploying ExternalDNS for Kubernetes

From the top level of the git repository:

* `sudo docker run -v $(pwd)/k8s:/files -it savvybi/superset-cluster-kops:0.1`
* `kops export kubecfg --name=${NAME}`
* Edit the cluster config to add required iam policies: `kops edit cluster ${NAME}`
* Copy the following yaml and add to the end of the cluster config in vi
```  
  additionalPolicies:
    node: |
      [
        {
          "Effect": "Allow",
          "Action": ["route53:ChangeResourceRecordSets"],
          "Resource": ["arn:aws:route53:::hostedzone/*"]
        },
        {
          "Effect": "Allow",
          "Action": ["route53:ListHostedZones","route53:ListResourceRecordSets"],
          "Resource": ["*"]
        }
      ]
```
* Run `kops update cluster ${NAME} --yes`
* Run `kops rolling-update cluster` to ensure that changes are applied
* From inside the superset-cluster-kops docker container, run the following to deploy the superset application:
`kubectl create -f /files/external-dns.yaml`
* From inside the superset-cluster-kops docker container, run the following to deploy a test nginx service:
`kubectl create -f /files/nginx.yaml`
* Wait for 5-10 minutes and then check that ExternalDNS has correctly created a new DNS entry in Route53, by browsing: `http://nginx.superset.savvybi.enterprises`

## Deploying superset application

From the top level of the git repository:
* `sudo docker run -v $(pwd)/superset-app:/files -it savvybi/superset-cluster-kops:0.1`
* From inside the superset-cluster-kops docker container, run the following to deploy the superset application:
* `kubectl create -f /files/superset.yaml`
* From inside the superset-cluster-kops docker container, run the following to get the external facing url:
* `kubectl describe service superset`
* you should see something like:
* `LoadBalancer Ingress:     a9c4e359f6d9711e8b31c068d3110b28-2094159502.ap-southeast-2.elb.amazonaws.com`
* browsing to that location will give the superset login page
* Wait for 10 minutes for ExternalDNS to generate a nice url and then browse to `http://superset-app.superset.savvybi.enterprises` - login with admin/pa55word

## Deploying zookeeper

If you have already created the k8s cluster, you will need to expand the cluster to at least 3 nodes.

From the top level of the git repository:
* `sudo docker run -v $(pwd)/druid:/files -it savvybi/superset-cluster-kops:0.1`
* From inside the superset-cluster-kops docker container, run the following:
* `kops export kubecfg --name=${NAME}`
* `kops edit ig nodes` and change to `maxSize: 3` and `minSize: 3`
* Run the zookeeper deployment `kubectl apply -f /files/zookeeper.yaml`