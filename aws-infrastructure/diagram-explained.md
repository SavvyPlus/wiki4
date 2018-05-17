<!-- TITLE: Diagram Explained -->
<!-- SUBTITLE: Use this to understand the process in which our dats is analysed and disected to have different levels of analysis -->

# Highlevel Diagram

 ![Architecture Diagram](/uploads/diagram/architecture-diagram.png "Architecture Diagram")

## Data lake 

Our Data Lake is where we place and upload all sorts of data,  in here you can find a list of the handlers that ingest and prepare the data to be able to be query using Athena. 
The structrue is simple , where each handler builds a S3 bucket and therefore are independenlty queried. 
The Data lake is combination of Highlevel and Deep Storage  (**Glacier** and **S3**), at this stage the systems and the analysis can use ML and DL , on a per bucket. 
**ML and DL**will be used mostly in larger datasets, at a simple to raw stage. 
**Athena** will be use to sandbox data and define the changes that need to happen for the data to be "Warehouse Ready".
**Glue**
**EC2**


## Data Warehouse
The Data Warehouse is where we ETL from the lake to the Warehouse to, in here multiple folders from different bucket are joined into one based on their required interaction, the idea is one bucket should have all necesary folders to eb able to be cross queries and also to create views and new tables based on more complex requirement and calcualtions. 
**S3**
**ML and DL** Now we can actually cross reference different sources of data for complex models to be able to run more efficienclty, also here we implement PyWren models to create spot and other forecast options
**Athena**
**Glue**
**EC2**


## Data Mart
The
**S3**
**ML and DL** 
**Athena**
**Glue**
**EC2**

