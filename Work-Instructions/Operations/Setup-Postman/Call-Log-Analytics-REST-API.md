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




