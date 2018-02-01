#Introduction

Postman can be used to simulate HTTP requests

##Activities

- Download Windows (x64) version [here](https://dl.pstmn.io/download/latest/win64)


---
##Get Azure Access tokens

Use following information to retrieve access token:
```
TenantID: 72f988bf-86f1-41af-91ab-2d7cd011db47
ClientID: 701b2b86-0880-417e-89de-6abafe0fd728
ClientSecret: eHhapd1ipgk6klHZBo1GDOuv2WSAZhqmA4a+Se8WPc8=
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






