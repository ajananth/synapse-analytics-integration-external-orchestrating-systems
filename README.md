# Synapse Analytics Integration with External Orchestrating Systems

Azure Synapse Analytics makes use of the Synapse Studio interface for enabling collaboration between data engineers, data scientists and end users. In addition to making use of Synapse Studio, an organisation could make use of interfaces made available by Azure such as the REST API framework, Azure CLI & SDKs to integrate Synapse Analytics with its own internal systems. By doing so, an external system could automate processes such as execution of pipelines & spark jobs while another could monitor the progress of jobs and action failures, etc.

In this article, I've captured the steps required to perform both management & data plane operations using Azure's REST API framework using a few examples. The testing was done using Postman as a client, but any application capable of making REST API calls can leverage the same process. The same concepts apply to other interfaces such as the Azure CLI, Python SDK, etc. so if the preference is to use those interfaces, equivalent methods can be called. Refer to the Appendix section for links.

## Create a Registered Application

The first step is to create a registered application in Azure AD. A secret needs to be created for the application, which will be used to retrieve a bearer token for using in subsequent API calls. Details on creating a registered application are available here - https://docs.microsoft.com/en-us/rest/api/azure/#register-your-client-application-with-azure-ad

For the purpose of this article, I've created a registered application called synapserestapiapp.

![alt text](images/ra.png?raw=true)

## Grant Permissions

Grant the service principal (SPN) appropriate access to Synapse Analytics. Access was granted to the synapserestapiapp SPN to the Synapse workspace in IAM and an appropriate RBAC role within the Synapse workspace as well.

## Retrieve a Token for Management Plane Operations

Azure AD authentication tokens for management plane operations are retrieved using the URL shown below (replace tenantId with your own).

```https://login.microsoftonline.com/{{tenantId}}/oauth2/v2.0/token```

Pass in the client credentials of the registered application along with the appropriate scope.

![alt text](images/mgmtpl.png?raw=true)

When the request is successful, a token is received which needs to be passed to subsequent management plane related API calls.

![alt text](images/atok.png?raw=true)

## Perform a Management Plane Operation (e.g. Retrieving Workspace Details)

To perform a management plane operation such as retrieving workspace details, make a call to the REST API and pass in the required parameters (in the call below, change subscriptionId, resourceGroupName and workspaceName to your own values).

```https://management.azure.com/subscriptions/{{subscriptionId}}/resourceGroups/{{resourceGroupName}}/providers/Microsoft.Synapse/workspaces/{{workspaceName}}?api-version=2019-06-01-preview```

Ensure you pass in the bearer token retrieved in the previous call.

![alt text](images/mtok.png?raw=true)

If the call is successful, workspace details should be retrieved in a JSON packet.

![alt text](images/wsps.png?raw=true)

## Retrieve a Token for Data Plane Operations

Retrieving a token for performing data plane opertions such as executing pipelines, monitoring pipeline status, executing spark jobs, etc. is done as shown below (replace tenantId with your own).

```https://login.microsoftonline.com/{{tenantId}}/oauth2/v2.0/token```

Pass in the client credentials of the registered application along with the appropriate scope (note dev.azuresynapse.net).

![alt text](images/dtok.png?raw=true)

When successful, the call returns a bearer token, which needs to be passed in subsequent API calls.

## Perform a Data Plane Operation (e.g. Executing a Pipeline)

To execute a Synapse pipeline, make use of the following REST API call (replace synapseWorkspace & pipelineName with your own).

```https://{{synapseWorkspace}}.dev.azuresynapse.net/pipelines/{{pipelineName}}/createRun?api-version=2019-06-01-preview&referencePipelineRunId=```

Ensure you pass in the bearer token retrieved from the previous method for authorisation.

![alt text](images/expl.png?raw=true)

When successful, this would return a Run ID, which can be used in a subsequent call to monitor the status of the pipeline run.

![alt text](images/runid.png?raw=true)

## Perform a Data Plane Operation (e.g. Monitoring Pipeline Status)

## Perform a Data Plane Operation (e.g. Executing a Spark Job)


### Appendix

* The full list of REST API methods for Synapse Analytics is available here - https://docs.microsoft.com/en-us/rest/api/synapse/
* The documentation on corresponding Azure CLI methods is available here - https://docs.microsoft.com/en-us/cli/azure/ext/synapse/synapse?view=azure-cli-latest
* The documentation on corresponding Python SDK methods is available here - https://docs.microsoft.com/en-us/python/api/overview/azure/synapse?view=azure-python
