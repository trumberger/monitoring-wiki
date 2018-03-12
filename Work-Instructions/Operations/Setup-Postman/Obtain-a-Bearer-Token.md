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

Copy the access token - you'll use it for subsequent requests to the Azure resource that you wish to access.
