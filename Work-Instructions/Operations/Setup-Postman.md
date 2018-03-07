#Introduction

Postman can be used to simulate HTTP requests

##Activities

- Download Windows (x64) version [here](https://dl.pstmn.io/download/latest/win64)


---
##Azure Access tokens
The REST endpoints for Azure resources are secured by the OAUTH 2 protocol. There are two steps to making requests to an Azure REST endpoint:

1) Obtain a Bearer Token (access token) for the resource you want to access
2) Use that token to make one or more calls to the endpoint

For more background:
Azure Active Directory allows _Users_ or _Services_ to authenticate with AAD and obtain access tokens. This identity (user or service) is known as a User Principal or a Service Principal. Typically in the monitoring solution, we use service principals - to see one, search Microsoft AAD Application Registrations for "SPN-Test-ApplicationInsights" as an example.

Each Service Principal is represented by an Application Id and a Key (assigned by AAD when the Service Principal is created) - this Application ID and Key must be used when you request a bearer token.

Other values you may need for retrieving an access token or accessing an endpoint:
```
TenantID:                    72f988bf-86f1-41af-91ab-2d7cd011db47
WorkspaceID (PROD):          e3eb539e-c40e-4c80-ae8f-19aa090713ed 

```
### Obtaining a Bearer Token via Postman
Create a new Request in Postman.
Set up the request with the following details:

```
Request Type: POST 
URL: https://login.microsoftonline.com/{TenantID}/oauth2/token?api-version=1.0


HEADERS:
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

BODY: (select 'x-www-form-urlencoded' from the options in Postman)
grant_type=client_credentials
resource={Resource type URI - see below}
client_id={Your Service Principal Application Id}
client_secret={Your Service Principal Key}

```


|Resource Type |Resource Uri |  
|:-----------|:-----------|
| Application Insights REST API| https://api.applicationinsights.io |  
| Azure Resource Manager REST API |https://management.core.windows.net/|
| Log Analytics REST API|https://api.loganalytics.io|

Once you have set up the request in Postman, click "Send" and you'll get a response similar to this:
```
{
    "token_type": "Bearer",
    "expires_in": "3599",
    "ext_expires_in": "0",
    "expires_on": "1520434317",
    "not_before": "1520430417",
    "resource": "https://api.applicationinsights.io",
    "access_token": "(very long string of characters)"
}
```

Copy the access token - you'll need it in the next steps.

The next sections show examples of calling various Azure endpoints. Each of these endpoints is rich in functionality, so please refer to the linked documentation for full details as each of the examples below is just a starting point.
 
###Azure Application Insights REST API

API documentation: <https://dev.applicationinsights.io/documentation/Overview>

**Example call to get request details that recorded in App Insights:**
```
GET https://api.applicationinsights.io/v1/apps/<application id>/metrics/requests/duration

HEADER
Authorization: Bearer {Access Token}
Content-Type: application/json

Notes: 
- The <application id> is the App Insights Api application Id. You find this by opening the App Insights resource in the Azure portal, clicking on "API Access" in the left hand menu, and copying the Application Id. It is NOT the Application Id of your SPN. 
```

### Azure Resource Manager REST API

<https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-rest-api>

```
GET
https://management.azure.com/{query}

HEADER
Authorization: Bearer {Access Token}
Content-Type: application/json
```

### Log Analytics REST API
<https://dev.loganalytics.io/documentation/Authorization/OAuth2>
```
POST
https://api.loganalytics.io/v1/workspaces/{workspaceID}/query


HEADER
Authorization: Bearer {Access Token}
Content-Type: application/json

BODY
{
    "query": "{query}"
}
```





