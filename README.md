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
paconn create --api-def apiDefinition.swagger.json --api-prop apiProperties.json --secret <client_secret>
```

## Supported Operations
The connector supports the following operations:
* `Search`: Searches documents, folders, and files (external documents) for a term and returns paginated results
* `Search Artefacts`: Return search results for a given query
