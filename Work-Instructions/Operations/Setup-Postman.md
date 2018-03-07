#Introduction

Postman can be used to simulate HTTP requests

##Activities

- Download Windows (x64) version [here](https://dl.pstmn.io/download/latest/win64)


---
##Azure Access tokens
The REST endpoints for Azure resources are secured by the [OAUTH 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-protocols-oauth-code) protocol. Before accessing the endpoint, you need to get an access token from Azure Active Directory. 

This guide first tells you how to get an Access Token (also known as a Bearer Token), and then shows some examples of calling Azure REST endpoints.

When reading the notes below, you will need to know the [Service Principal](/Work-Instructions/Operations/Setup-Postman) Application ID and Key that you want to use, as well as some of the following values:
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





