## Panviva Connector
Panviva provides a powerful and very extensive REST API. Using this API, you can access and manage knwledge stores in your Panviva instances. This connector allows you to  leverage the same knowledge within your application, or in your process automation.



## Prerequisites
You will need the following to proceed:
* A Microsoft Power Apps or Power Automate plan with custom connector feature
* An Panviva subscription & a 
* The Power platform CLI tools

## Building the connector 
Since the Panviva APIs are secured, you will need
1. Access to a Panviva Instance (also known as a Tenant)
2. A developer account on the Panviva Developer Portal [https://dev.panviva.com](https://dev.panviva.com)
3. An active Panviva API Subscription (also known as an API Plan) and valid Panviva API Credentials
After that is completed, you can create and test the connector.

### Deploying the sample
Run the following commands and follow the prompts:

```paconn
paconn create --api-def apiDefinition.swagger.json --api-prop apiProperties.json 
```

## Supported Actions
The connector supports the following Actions:
* **Search Operations**
  * `Search`: Searches documents, folders, and files (external documents) for a term and returns paginated results
  * `Search Artefacts`: Return search results for a given query
* **Live Operations**
  * `Live CSH`: Present a CSH search result page of the passing query on Panviva client to specified user on Panviva client
  * `Live Document`: Present a document page to specified user on Panviva client\
  * `Live Search`: Present a search result page of the passing query on Panviva client to specified user on Panviva
* **Document Operations**
  * `Document`: Return a document using the document ID provided
  * `Document Containers`: Return a list of containers using the document ID provided
  * `Document Container Relationships`: Return a list of the parent-child relationship between each container for the document ID provided
  * `Container`: Return a container using the container ID provided
  * `Document Translations`: Return a list of all translations (per language and locale) of a Panviva document
* **Resource Operations**
  * `Artefact`: Return an artefact using the ID provided
  * `File`: Returns a file (external document) from Panviva
  * `Folder`: Return information about a Panviva folder and references to each of its direct children
  * `Folder Children`: Gets all the immediate children of a Panviva folder, not including grandchildren. Children can be folders, documents, or files (external documents)
  * `Folder Translations`: Gets all the translations of a Panviva folder, along with each translated folders respective children
  * `Folder Root`: Gets the root/home folder in all of Panviva, which can be drilled into using the Get Folder Children endpoint. Note this endpoint was formerly referred to as the 'Folder Search' endpoint
  * `Image`: Returns an image from Panviva. Image data is represented as a base64 string
  
