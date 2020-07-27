# Panviva
Wouldn't it be great if you could share information seamlessly? This connector allows you to push your knowledge further and consume a complete list of Panviva's API offerings within your application, or in your process automation. Explore the following APIs with this connector:
* **Content APIs** perform resource related operations , e.g. `document`, `folder`, `file`, `container`, `image`.
* **Live APIs** enable real-time communications with online users on our client application.
* **Artefact APIs** interact with curated Panviva content, created by the Digital Orchestrator.

## Prerequisites

To use the Panviva connector, you must have:
1. Access to a Panviva Instance (also known as a Tenant)
2. A developer account on the Panviva Developer Portal [https://dev.panviva.com](https://dev.panviva.com)
3. An active Panviva API Subscription (also known as an API Plan) and valid Panviva API Credentials

If you are not a customer or need help visit [www.panviva.com/support](https://www.panviva.com/support).

## How to get credentials

Follow steps below to get your API Key & API Instance.

If you see an error while using the connector you may look up the error code for more information. Note the HTTP status code in the documentation may be slightly different than what you see in Power Automate or Power Apps, please use the Error Code field for lookup purposes.

To get your API Key you must:
1. Sign into the Panviva Developer Portal at [https://dev.panviva.com](https://dev.panviva.com)
2. Navigate to your Profile (click your name then click "Profile" from the top navigation bar)
3. Your should now see your Api Key under "Your Subscriptions" section of your profile.

To get your API Instance you must:
1. Sign into the Panviva Developer Portal at [https://dev.panviva.com](https://dev.panviva.com)
2. Navigate to your API (click "APIS" from the top navigation bar)
3. You should now see your API Instance under your API Suite (look for "*The instance name for the API Suite is*")

## Known issues and limitations

Note that your throttling limits will be based on the type of API Subscription (or API Plan) to which you've subscribed.

To find your Quota or Rate Limit you can:
1. Sign into the Panviva Developer Portal at [https://dev.panviva.com](https://dev.panviva.com)
2. Navigate to your Profile (click your name then click "Profile" from the top navigation bar)
3. Go to your Api Plan under "Your Subscriptions" section of your profile
4. You should now see the details of your plan (look for "*...will be able to run __ calls/minute up to a maximum of ___ calls/month...*")


## Actions
The connector supports the following Actions:
* [**Search Operations**](#search-operations)
  * [`Search`](#search-instanceoperationssearch): Searches documents, folders, and files (external documents) for a term and returns paginated results
  * [`Search Artefacts`](#search-artefacts-instanceoperationsartefactnls): Return search results for a given query
* [**Live Operations**](#live-operations)
  * [`Live CSH`](#live-csh-instanceoperationslivecsh): Present a CSH search result page of the passing query on Panviva client to specified user on Panviva client
  * [`Live Document`](#live-document-instanceoperationslivedocument): Present a document page to specified user on Panviva client\
  * [`Live Search`](#live-search-instanceoperationslivesearch): Present a search result page of the passing query on Panviva client to specified user on Panviva
* [**Document Operations**](#document-operations)
  * [`Document`](#document-instanceresourcesdocumentid): Return a document using the document ID provided
  * [`Document Containers`](#document-containers-instanceresourcesdocumentidcontainers): Return a list of containers using the document ID provided
  * [`Document Container Relationships`](#document-container-relationships-instanceresourcesdocumentidcontainersrelationships): Return a list of the parent-child relationship between each container for the document ID provided
  * [`Container`](#container-instanceresourcescontainerid): Return a container using the container ID provided
  * [`Document Translations`](#document-translations-instanceresourcesdocumentidtranslations): Return a list of all translations (per language and locale) of a Panviva document
* [**Resource Operations**](#resource-operations)
  * [`Artefact`](#artefact-instanceresourcesartefactid): Return an artefact using the ID provided
  * [`Artefact Categories`](#artefact-categories-instanceresourcesartefactcategory): Gets a list of all available artefact categories
  * [`File`](#file-instanceresourcesfileid): Returns a file (external document) from Panviva
  * [`Folder`](#folder-instanceresourcesfolderid): Return information about a Panviva folder and references to each of its direct children
  * [`Folder Children`](#folder-children-instanceresourcesfolderidchildren): Gets all the immediate children of a Panviva folder, not including grandchildren. Children can be folders, documents, or files (external documents)
  * [`Folder Translations`](#folder-translations-instanceresourcesfolderidtranslations): Gets all the translations of a Panviva folder, along with each translated folders respective children
  * [`Folder Root`](#folder-root-instanceresourcesfolderroot): Gets the root/home folder in all of Panviva, which can be drilled into using the Get Folder Children endpoint. Note this endpoint was formerly referred to as the 'Folder Search' endpoint
  * [`Image`](#image-instanceresourcesimageid): Returns an image from Panviva. Image data is represented as a base64 string

The abovementioned actions have been described in detail below.

## Search Operations

### Search `/{instance}/operations/search`

#### GET

##### Description:

Searches documents, folders, and files (external documents) for a term and returns paginated results

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| term | query | The word or phrase to be searched for | Yes | string |
| pageOffset | query | The pagination offset to denote the number of initial search results to skip. For example, pageOffset of 100 and pageLimit of 10 would return records 101-110. | No | integer |
| pageLimit | query | The number of records to return. Must be an integer between 0 and 1000. | No | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetSearchResponse](#getsearchresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Search Artefacts `/{instance}/operations/artefact/nls`

#### GET

##### Description:

Return search results for a given query

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| simplequery | query | Natural language query string. For example: ```Action Movies```. (Note: Use simplequery OR advancedquery, not both.) | No | string |
| advancedquery | query | Query string written in Lucene query syntax. For example: ```films AND "a story"```. (Note: Use simplequery OR advancedquery, not both.) | No | string |
| filter | query | Accepts a Lucene-formatted filter string. Examples: ```category eq 'Mortgages'```, ```panvivaDocumentVersion gt '8'```. (Filterable fields include dateCreated, dateModified, dateDeleted, categoryJson, queryVariationsJson, title, category, primaryQuery, isDeleted, timestamp, panvivaDocumentId, panvivaDocumentVersion, id) | No | string |
| channel | query | Return response for a specific channel, instead of the default | No | string |
| pageOffset | query | The pagination offset to denote the number of initial search results to skip. For example, pageOffset of 100 and pageLimit of 10 would return records 101-110. | No | integer |
| pageLimit | query | The number of records to return. Must be an integer between 0 and 1000. | No | integer |
| facet | query | Accepts a Lucene-formatted facet string. Examples: ```facet=Category,count:10&amp;facet=Rating```. (Facetable fields include metaData/values) | No | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetSearchArtefactResponse](#getsearchartefactresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |




## Live Operations
### Live CSH `/{instance}/operations/live/csh`

#### POST

##### Description:

Present a CSH search result page of the passing query on Panviva client to specified user on Panviva client

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| postLiveCshRequest | body | JSON object containing information required to perform a live activity<span>:</span> | No | [PostLiveCshRequest](#postlivecshrequest) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 202 | The request has been accepted for processing, but processing has not yet completed. There is a possibility that the request will fail, if it is disallowed when processing actually takes place. There is no facility for sending a completion-status code from this operation. | [PostLiveCshResponse](#postlivecshresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Live Document `/{instance}/operations/live/document`

#### POST

##### Description:

Present a document page to specified user on Panviva client

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| postLiveDocumentRequest | body | JSON object containing information required to perform a live activity<span>:</span> | No | [PostLiveDocumentRequest](#postlivedocumentrequest) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 202 | The request has been accepted for processing, but processing has not yet completed. There is a possibility that the request will fail, if it is disallowed when processing actually takes place. There is no facility for sending a completion-status code from this operation. | [PostLiveDocumentResponse](#postlivedocumentresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Live Search `/{instance}/operations/live/search`

#### POST

##### Description:

Present a search result page of the passing query on Panviva client to specified user on Panviva client

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| postLiveSearchRequest | body | JSON object containing information required to perform a live activity<span>:</span> | No | [PostLiveSearchRequest](#postlivesearchrequest) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 202 | The request has been accepted for processing, but processing has not yet completed. There is a possibility that the request will fail, if it is disallowed when processing actually takes place. There is no facility for sending a completion-status code from this operation. | [PostLiveSearchResponse](#postlivesearchresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |


## Document Operations

### Document `/{instance}/resources/document/{id}`

#### GET

##### Description:

Return a document using the document ID provided

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | A document unique identifier, Document ID. If a document is a translated document, this value represents Internal ID or IID in Panviva API v1. | Yes | string |
| version | query | Request the API to return a particular version of the specified document. | No | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetDocumentResponse](#getdocumentresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Document Containers `/{instance}/resources/document/{id}/containers`

#### GET

##### Description:

Return a list of containers using the document ID provided

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The internal id (IID) of a Panviva document | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetDocumentContainersResponse](#getdocumentcontainersresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |


### Document Container Relationships `/{instance}/resources/document/{id}/containers/relationships`

#### GET

##### Description:

Return a list of the parent-child relationship between each container for the document ID provided

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The internal id (IID) of a Panviva document | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetDocumentContainerRelationshipsResponse](#getdocumentcontainerrelationshipsresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |


### Container `/{instance}/resources/container/{id}`

#### GET

##### Description:

Return a container using the container ID provided

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The id of a document container | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetContainerResponse](#getcontainerresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Document Translations `/{instance}/resources/document/{id}/translations`

#### GET

##### Description:

Return a list of all translations (per language and locale) of a Panviva document

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The internal id (IID) of a Panviva document. | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetDocumentTranslationsResponse](#getdocumenttranslationsresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |


## Resource Operations

### Artefact `/{instance}/resources/artefact/{id}`

#### GET

##### Description:

Return an artefact using the ID provided

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | Format - uuid. The id (ID) of an artefact | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetResponseResponse](#getresponseresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |


### Artefact Categories `/{instance}/resources/artefactcategory`

#### GET

##### Description:

Gets a list of all available artefact categories

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetArtefactCategoriesResponse](#getartefactcategoriesresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

#### POST

##### Description:

Creates a category for classifying artefacts

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| postArtefactCategoryRequest | body | JSON object containing the category name | No | [PostArtefactCategoryRequest](#postartefactcategoryrequest) |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Success | [PostArtefactCategoryResponse](#postartefactcategoryresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### File `/{instance}/resources/file/{id}`

#### GET

##### Description:

Returns a file (external document) from Panviva

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The internal id (IID) of a Panviva file (external document) | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetFileResponse](#getfileresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Folder `/{instance}/resources/folder/{id}`

#### GET

##### Description:

Return information about a Panviva folder and references to each of its direct children

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The internal id (IID) of a Panviva folder | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetFolderResponse](#getfolderresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Folder Children `/{instance}/resources/folder/{id}/children`

#### GET

##### Description:

Gets all the immediate children of a Panviva folder, not including grandchildren. Children can be folders, documents, or files (external documents)

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The internal id (IID) of a Panviva folder | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetFolderChildrenResponse](#getfolderchildrenresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Folder Translations `/{instance}/resources/folder/{id}/translations`

#### GET

##### Description:

Gets all the translations of a Panviva folder, along with each translated folders respective children

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The internal id (IID) of a Panviva folder | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetFolderTranslationsResponse](#getfoldertranslationsresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Folder Root `/{instance}/resources/folder/root`

#### GET

##### Description:

Gets the root/home folder in all of Panviva, which can be drilled into using the Get Folder Children endpoint. Note this endpoint was formerly referred to as the 'Folder Search' endpoint

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetFolderRootResponse](#getfolderrootresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |

### Image `/{instance}/resources/image/{id}`

#### GET

##### Description:

Returns an image from Panviva. Image data is represented as a base64 string

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| instance | path | The instance name as shown on the Panviva Developer Portal. | Yes | string |
| id | path | The id of a Panviva image | Yes | integer |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The operation is successful and returns with the requested resource. An example of a successful response can be seen in the Sample payload. | [GetImageResponse](#getimageresponse) |
| 400 | Bad Request - The request could not be understood by the server due to malformed syntax. The client should not repeat the request without modifications. |  |
| 403 | Out of call volume quota. |  |
| 404 | Document not found - The server has not found anything matching the request URI. |  |
| 405 | Method Not Allowed - The method specified in the request is not allowed for the resource identified by the request URI.  |  |
| 406 | Not Acceptable - The resource identified by the request is only capable of generating response entities which have content characteristics not acceptable according to the accept headers sent in the request. If accept headers is specified, application/json must be the only media type. |  |
| 415 | Unsupported Media Type - The server is refusing to service the request because the entity of the request is in a format not supported by the requested resource for the requested method. The only supported media type is application/json. |  |
| 429 | Too many requests - The number of requests has reached the plan’s rate limit. |  |
| 503 | Service Unavailable - Panviva servers are under maintenance. |  |


### Models


#### Link

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string |  | No |
| rel | string |  | No |
| type | string |  | No |

#### ResourceSearchResult

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| type | string |  | No |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| matchedFields | [ string ] |  | No |
| snippet | string |  | No |
| language | string |  | No |
| links | [ [Link](#link) ] |  | No |

#### GetSearchResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| results | [ [ResourceSearchResult](#resourcesearchresult) ] |  | No |
| total | integer |  | No |
| links | [ [Link](#link) ] |  | No |

#### StringInt64NullableKeyValuePair

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| key | string |  | No |
| value | long |  | No |

#### Facet

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| field | string |  | No |
| groups | [ [StringInt64NullableKeyValuePair](#stringint64nullablekeyvaluepair) ] |  | No |

#### ResponseSection

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| mediaType | string |  | No |
| text | string |  | No |
| href | string |  | No |
| resourceLocation | string |  | No |

#### Category

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |
| id | integer |  | No |
| dateCreated | dateTime |  | No |
| dateModified | dateTime |  | No |

#### MetaDataValueDetails

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| values | [ string ] |  | No |
| dataType | string |  | No |

#### QueryVariation

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | integer |  | No |
| query | string |  | No |

#### SearchResult

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string (uuid) |  | No |
| content | [ [ResponseSection](#responsesection) ] |  | No |
| category | [Category](#category) |  | No |
| metaData | object |  | No |
| searchScore | number |  | No |
| links | [ [Link](#link) ] |  | No |
| queryVariations | [ [QueryVariation](#queryvariation) ] |  | No |
| primaryQuery | string |  | No |
| panvivaDocumentId | integer |  | No |
| panvivaDocumentVersion | integer |  | No |
| title | string |  | No |

#### GetSearchArtefactResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| facets | [ [Facet](#facet) ] |  | No |
| results | [ [SearchResult](#searchresult) ] |  | No |
| total | integer |  | No |

#### PostLiveCshRequest

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| username | string | The Panviva user to whom you wish to send the result. (Note: Use username OR userId, not both.) | No |
| userId | string | The numeric ID of the user to whom you wish to send the result. (Note: Use username OR userId, not both.) | No |
| query | string | The CSH term to search for. | No |
| showFirstResult | boolean | True to immediately open the first document found, or false to show the list of results. | No |
| maximizeClient | boolean | True/False depending on whether you want the Panviva client to maximize on the user's desktop, when the document is delivered. | No |

#### PostLiveCshResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| PostLiveCshResponse | object |  |  |

#### PostLiveDocumentRequest

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| username | string | The Panviva user to whom you wish to send the result. (Note: Use username OR userId, not both.) | No |
| userId | string | The numeric ID of the user to whom you wish to send the result. (Note: Use username OR userId, not both.) | No |
| id | string | The Document ID of the Panviva Document you wish to send. | No |
| location | string | The Section ID you would like the user to see, when the specified document is opened. | No |
| maximizeClient | boolean | True/False depending on whether you want the Panviva client to maximize on the user's desktop, when the document is delivered. | No |

#### PostLiveDocumentResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| PostLiveDocumentResponse | object |  |  |

#### PostLiveSearchRequest

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| username | string | The Panviva user to whom you wish to send the result. (Note: Use username OR userId, not both.) | No |
| userId | string | The numeric ID of the user to whom you wish to send the result. (Note: Use username OR userId, not both.) | No |
| query | string | The term to search for. | No |
| maximizeClient | boolean | True/False depending on whether you want the Panviva client to maximize on the user's desktop, when the document is delivered. | No |
| showFirstResult | boolean | True to immediately open the first document found, or false to show the list of results. | No |

#### PostLiveSearchResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| PostLiveSearchResponse | object |  |  |

#### GetContainerResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| body | string |  | No |

#### Tag

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |
| value | string |  | No |

#### Training

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| failureFeedback | string |  | No |
| forcePageSequence | boolean |  | No |
| forceQuestionSequence | boolean |  | No |
| passingScore | integer |  | No |
| successFeedback | string |  | No |

#### GetDocumentResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| version | integer |  | No |
| language | string |  | No |
| tags | [ [Tag](#tag) ] |  | No |
| hidden | boolean |  | No |
| source | string |  | No |
| type | string |  | No |
| release | integer |  | No |
| released | boolean |  | No |
| copyright | string |  | No |
| classification | string |  | No |
| status | string |  | No |
| percentage | integer |  | No |
| releaseDate | dateTime |  | No |
| layout | string |  | No |
| training | [Training](#training) |  | No |
| keywords | [ string ] |  | No |
| cshKeywords | [ string ] |  | No |
| updatedDate | dateTime |  | No |
| createdDate | dateTime |  | No |
| reusableContent | boolean |  | No |
| changeNote | string |  | No |
| links | [ [Link](#link) ] |  | No |

#### Channel

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |

#### ResponseVariation

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| content | [ [ResponseSection](#responsesection) ] |  | No |
| channels | [ [Channel](#channel) ] |  | No |
| id | integer |  | No |
| dateCreated | dateTime |  | No |
| dateModified | dateTime |  | No |

#### GetResponseResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| links | [ [Link](#link) ] |  | No |
| title | string |  | No |
| content | [ [ResponseSection](#responsesection) ] |  | No |
| variations | [ [ResponseVariation](#responsevariation) ] |  | No |
| category | [Category](#category) |  | No |
| primaryQuery | string |  | No |
| queryVariations | [ [QueryVariation](#queryvariation) ] |  | No |
| panvivaDocumentId | integer |  | No |
| panvivaDocumentVersion | integer |  | No |
| metaData | object |  | No |
| id | string (uuid) |  | No |
| dateCreated | dateTime |  | No |
| dateModified | dateTime |  | No |

#### Container

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| body | string |  | No |

#### GetDocumentContainersResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| containers | [ [Container](#container) ] |  | No |

#### ContainerRelationship

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| parent | string |  | No |
| children | [ string ] |  | No |
| taskFlow | string |  | No |

#### GetDocumentContainerRelationshipsResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| relationships | [ [ContainerRelationship](#containerrelationship) ] |  | No |

#### Document

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| version | integer |  | No |
| language | string |  | No |
| tags | [ [Tag](#tag) ] |  | No |
| hidden | boolean |  | No |
| source | string |  | No |
| type | string |  | No |
| release | integer |  | No |
| released | boolean |  | No |
| copyright | string |  | No |
| classification | string |  | No |
| status | string |  | No |
| percentage | integer |  | No |
| releaseDate | dateTime |  | No |
| layout | string |  | No |
| training | [Training](#training) |  | No |
| keywords | [ string ] |  | No |
| cshKeywords | [ string ] |  | No |
| updatedDate | dateTime |  | No |
| createdDate | dateTime |  | No |
| reusableContent | boolean |  | No |
| changeNote | string |  | No |
| links | [ [Link](#link) ] |  | No |

#### GetDocumentTranslationsResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| translations | [ [Document](#document) ] |  | No |
| origin | string |  | No |

#### GetFileResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| version | integer |  | No |
| language | string |  | No |
| tags | [ [Tag](#tag) ] |  | No |
| hidden | boolean |  | No |
| source | string |  | No |
| type | string |  | No |
| content | string |  | No |
| fileName | string |  | No |
| release | integer |  | No |
| released | boolean |  | No |
| copyright | string |  | No |
| classification | string |  | No |
| status | string |  | No |
| percentage | integer |  | No |
| releaseDate | dateTime |  | No |
| keywords | [ string ] |  | No |
| cshKeywords | [ string ] |  | No |
| changeNote | string |  | No |
| updatedDate | dateTime |  | No |
| createdDate | dateTime |  | No |

#### GetFolderResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| version | integer |  | No |
| language | string |  | No |
| tags | [ [Tag](#tag) ] |  | No |
| hidden | boolean |  | No |
| source | string |  | No |
| type | string |  | No |
| links | [ [Link](#link) ] |  | No |

#### Resource

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| version | integer |  | No |
| language | string |  | No |
| tags | [ [Tag](#tag) ] |  | No |
| hidden | boolean |  | No |
| source | string |  | No |
| type | string |  | No |

#### GetFolderChildrenResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| children | [ [Resource](#resource) ] |  | No |

#### Folder

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| version | integer |  | No |
| language | string |  | No |
| tags | [ [Tag](#tag) ] |  | No |
| hidden | boolean |  | No |
| source | string |  | No |
| type | string |  | No |
| links | [ [Link](#link) ] |  | No |

#### GetFolderTranslationsResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| translations | [ [Folder](#folder) ] |  | No |

#### GetFolderRootResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| description | string |  | No |
| version | integer |  | No |
| language | string |  | No |
| tags | [ [Tag](#tag) ] |  | No |
| hidden | boolean |  | No |
| source | string |  | No |
| type | string |  | No |
| links | [ [Link](#link) ] |  | No |

#### GetImageResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| width | integer |  | No |
| height | integer |  | No |
| size | integer |  | No |
| contentType | string |  | No |
| content | string |  | No |

#### ArtefactCategory

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | integer |  | No |
| categoryName | string |  | No |

#### GetArtefactCategoriesResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| categories | [ [ArtefactCategory](#artefactcategory) ] |  | No |

#### PostArtefactCategoryRequest

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |

#### PostArtefactCategoryResponse

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| categoryId | integer |  | No |
| categoryName | string |  | No |
