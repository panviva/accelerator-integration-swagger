# Panviva
Wouldn't it be great if you could share information seamlessly? This connector allows you to push your knowledge further and consume a complete list of Panviva's API offerings.

**Content APIs** perform resource related operations , e.g. `document`, `folder`, `file`, `container`, `image`.

**Live APIs** enable real-time communications with online users on our client application.

**Artefact APIs** interact with curated Panviva content, created by the Digital Orchestrator.

## Prerequisites

... Pending

Provide information about any prerequisites that are required to use this connector. For example, an account on your website, a paid service plan, and so on. 

## How to get credentials

... Pending

Provide detailed information about how a user can get credentials to leverage the connector. Where possible, this should be step-by-step instructions with links pointing to relevant parts of your website.

If your connector doesn't require authentication, this section can be removed.

## Known issues and limitations

... Pending

If your connector has any known issues and limitations, include a detailed description of them here.

## Technical Details
### Version: 1.0

### Security
**apiKeyHeader**  

|apiKey|*API Key*|
|---|---|
|Name|Ocp-Apim-Subscription-Key|
|In|header|

## Operations

... Pending 

Add a table/list here for ease of use.

### /{instance}/operations/search

#### GET
##### Summary:

Search

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

### /{instance}/operations/artefact/nls

#### GET
##### Summary:

Search Artefacts

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

### /{instance}/operations/live/csh

#### POST
##### Summary:

Live CSH

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

### /{instance}/operations/live/document

#### POST
##### Summary:

Live Document

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

### /{instance}/operations/live/search

#### POST
##### Summary:

Live Search

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

### /{instance}/resources/container/{id}

#### GET
##### Summary:

Container

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

### /{instance}/resources/document/{id}

#### GET
##### Summary:

Document

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

### /{instance}/resources/artefact/{id}

#### GET
##### Summary:

Artefact

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

### /{instance}/resources/document/{id}/containers

#### GET
##### Summary:

Document Containers

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

### /{instance}/resources/document/{id}/containers/relationships

#### GET
##### Summary:

Document Container Relationships

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

### /{instance}/resources/document/{id}/translations

#### GET
##### Summary:

Document Translations

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

### /{instance}/resources/file/{id}

#### GET
##### Summary:

File

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

### /{instance}/resources/folder/{id}

#### GET
##### Summary:

Folder

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

### /{instance}/resources/folder/{id}/children

#### GET
##### Summary:

Folder Children

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

### /{instance}/resources/folder/{id}/translations

#### GET
##### Summary:

Folder Translations

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

### /{instance}/resources/folder/root

#### GET
##### Summary:

Folder Root

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

### /{instance}/resources/image/{id}

#### GET
##### Summary:

Image

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

### /{instance}/resources/artefactcategory

#### GET
##### Summary:

Get Artefact Categories

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
##### Summary:

Create Artefact Category

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
