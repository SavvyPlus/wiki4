<!-- TITLE: Superset Kubernetes -->
<!-- SUBTITLE: A quick summary of Superset Kubernetes -->

# Superset on Kubernetes
Savvy will use Superset [https://github.com/apache/incubator-superset] to create a business intelligence dashboard for viewing the reports that are currently available in PowerBI.

## Deployment Platform
We will deploy Superset on Kubernetes [https://kubernetes.io/] so that we can autoscale the nodes that Superset runs on to support multiple users/businesses.

### Kubernetes on AWS
![K8s](/uploads/untitled-diagram.png "K8s")in 
Kubernetes is a container orchestration platform that will automatically move docker containers from a container host that is failing to a new host or can spin up a new instance of a container in a new host.