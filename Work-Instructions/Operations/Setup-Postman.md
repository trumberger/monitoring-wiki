#Introduction

Postman can be used to simulate HTTP requests

##Activities

- Download Windows (x64) version [here](https://dl.pstmn.io/download/latest/win64)


---
##Get Azure Access tokens

Use following information to retrieve access token:
```
TenantID:                    72f988bf-86f1-41af-91ab-2d7cd011db47
WorkspaceID (PROD):          e3eb539e-c40e-4c80-ae8f-19aa090713ed 

```

### Azure Resource Manager REST API

<https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-rest-api>

```
POST 
https://login.microsoftonline.com/{TenantID}/oauth2/token?api-version=1.0

HEADER
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

BODY
grant_type=client_credentials
resource=https://management.core.windows.net/
client_id={ClientID}
client_secret={ClientSecret}

```
Copy the access token and use the access token to query the ARM TEST API
```
GET
https://management.azure.com/{query}

HEADER
Authorization: Bearer {Acces Token}
Content-Type: application/json
```

### Log Analytics REST API
<https://dev.loganalytics.io/documentation/Authorization/OAuth2>

**Access Token**
```
POST 
https://login.microsoftonline.com/{TenantID}/oauth2/token

HEADER
Content-Type: application/x-www-form-urlencoded

BODY
grant_type=client_credentials
resource=https://api.loganalytics.io
client_id={ClientID}
client_secret={ClientSecret}
```
Copy the access token and use the access token to query the Log Analytics API
```
POST
https://api.loganalytics.io/v1/workspaces/{workspaceID}/query


HEADER
Authorization: Bearer {Acces Token}
Content-Type: application/json

BODY
{
    "query": "{query}"
}
```





