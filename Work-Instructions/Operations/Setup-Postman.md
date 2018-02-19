#Introduction

Postman can be used to simulate HTTP requests

##Activities

- Download Windows (x64) version [here](https://dl.pstmn.io/download/latest/win64)


---
##Get Azure Access tokens

Use following information to retrieve access token:
```
TenantID: 72f988bf-86f1-41af-91ab-2d7cd011db47

RESOURCE MANAGER
ClientID: 701b2b86-0880-417e-89de-6abafe0fd728
ClientSecret: eHhapd1ipgk6klHZBo1GDOuv2WSAZhqmA4a+Se8WPc8=

LOG ANALYTICS
Name: SPN-STAG-QueryOMS-BPL-MON 
ReplyURL: https://api.loganalytics.io
ClientID: d410757f-c2c9-4346-8ba8-764379053376
ClientSecret: z9T//2o44AZH5Zu+b2v5r/fp8H/QZfGCeF4uvdor8TE=

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
client_id=701b2b86-0880-417e-89de-6abafe0fd728
client_secret=eHhapd1ipgk6klHZBo1GDOuv2WSAZhqmA4a+Se8WPc8=

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

**Authentication Code**
````
GET
https://login.microsoftonline.com/{TenantID}/oauth2/authorize

BODY
client_id={ClientID}
response_type=code
redirect_uri={ReplyURL}
resource=https://api.loganalytics.io
````

**Access Token**
```
POST 
https://login.microsoftonline.com/{TenantID}/oauth2/token

HEADER
Content-Type: application/x-www-form-urlencoded

BODY
grant_type=authorization_code
client_id={ClientID}
code=AUTHORIZATION_CODE
redirect_uri={ReplyURL}
resource=https://api.loganalytics.io
client_secret={ClientSecret}
```





