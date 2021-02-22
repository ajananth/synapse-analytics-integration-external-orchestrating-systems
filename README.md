# Synapse Analytics Integration with External Systems

Azure Synapse Analytics makes use of the Synapse Studio interface for enabling collaboration between data engineers, data scientists and end users. In addition to making use of Synapse Studio, an organisation could make use of interfaces made available by Azure such as the REST API framework, Azure CLI & SDKs to integrate Synapse Analytics with its own internal systems. By doing so, an external system could automate processes such as execution of pipelines & spark jobs while another could monitor the progress of jobs and action failures, etc.

In this article, I've captured the steps required to perform both management & data plane operations using Azure's REST API framework using a few examples. The testing was done using Postman as a client, but any application capable of making REST API calls can leverage the same process. The same concepts apply to other interfaces such as the Azure CLI, Python SDK, etc. so if the preference is to use those interfaces, equivalent methods can be called. Refer to the Appendix section for links.

## Create a Registered Application

The first step is to create a registered application in Azure AD. A secret needs to be created for the application, which will be used to retrieve a bearer token for using in subsequent API calls. Details on creating a registered application are available here - https://docs.microsoft.com/en-us/rest/api/azure/#register-your-client-application-with-azure-ad

For the purpose of this article, I've created a registered application called synapserestapiapp.

![alt text](images/ra.png?raw=true)

## Grant Permissions

Grant the service principal (SPN) appropriate access to Synapse Analytics. For the purpose of this article, I've given then synapserestapiapp SPN Owner access in IAM to the Synapse workspace to perform all management plane operations and the Synapse Administrator RBAC role within the Synapse workspace so that it can perform all data plane operations. In a production environment, appropriate permissions need to be granted to ensure the SPN only has the access it requires.

#### IAM
![alt text](images/iam.png?raw=true)

#### Workspace
![alt text](images/ws.png?raw=true)

## Retrieve a Token for Management Plane Operations



## Perform a Management Plane Operation (Retrieving Workspace Details)

## Retrieve a Token for Data Plane Operations

## Perform a Data Plane Operation (Executing a Pipeline)

## Perform a Data Plane Operation (Monitoring Pipeline Status)

## Perform a Data Plane Operation (Executing a Spark Job)


### Appendix

* The full list of REST API methods for Synapse Analytics is available here - https://docs.microsoft.com/en-us/rest/api/synapse/
* The documentation on corresponding Azure CLI methods is available here - https://docs.microsoft.com/en-us/cli/azure/ext/synapse/synapse?view=azure-cli-latest
* The documentation on corresponding Python SDK methods is available here - https://docs.microsoft.com/en-us/python/api/overview/azure/synapse?view=azure-python
