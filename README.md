# Synapse Analytics Integration with External Systems

Many organisations are currently leveraging Azure Synapse Analytics to bring together their data integration, warehousing and analytics operations into a single unified platform. Synapse Analytics makes use of the Synapse Studio interface for data engineers, data scientists and end users to collaborate together. In addition to making use of the Synapse Studio interface, an organisation could also make use of interfaces made available by Azure such as the REST API framework, Azure CLI & SDKs to integrate Synapse Analytics with its own internal systems. By doing so, an external system could automate processes such as execution of pipelines & spark jobs while another could monitor the progress of jobs and action failures, etc.

In this article, I've captured the steps required to perform both management & data plane operations using the REST API framework using a few examples. The testing was done using Postman as a client, but any application capable of making REST API calls can leverage the same process. The same concepts apply to other interfaces such as the Azure CLI, Python SDK, etc.

## Create a Registered Application

## Grant Permissions

## Retrieve a Token for Management Plane Operations

## Perform a Management Plane Operation (Retrieving Workspace Details)

## Retrieve a Token for Data Plane Operations

## Perform a Data Plane Operation (Publishing a SQL Script)

### Appendix

* The full list of REST API methods for Synapse Analytics is available here - https://docs.microsoft.com/en-us/rest/api/synapse/
* The documentation on Azure CLI methods is available here - https://docs.microsoft.com/en-us/cli/azure/ext/synapse/synapse?view=azure-cli-latest
* The documentation on the Python SDK methods is available here - https://docs.microsoft.com/en-us/python/api/overview/azure/synapse?view=azure-python
