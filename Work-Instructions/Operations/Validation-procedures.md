# Validate Monitoring Agent - Checklist

Verify there are no errors in Logic App. It should have an all green successful execution runs. Something like this:

![Screen Shot 2018-05-09 at 11.56.31 AM.png](.attachments/Screen%20Shot%202018-05-09%20at%2011.56.31%20AM-eeb57a98-339e-4d2b-8b71-fe863dc456fa.png)

If you see errors, like the example below:

![Screen Shot 2018-04-24 at 5.01.38 PM.png](.attachments/Screen%20Shot%202018-04-24%20at%205.01.38%20PM-b6345553-b8c7-4965-9751-8995fd5271e5.png)
Please review the following items:
- Verify which part of the Logic App is causing errors (on each block of the Logic App, look for the red exclamation mark)

Example Errors:
- Error retrieving Error Definitions:
Message: NotFound
Status Code : 404
Example payload (Response):
`{
    "statusCode": 404,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "8a72d04d-48fd-4a6f-a005-1c3047f50f40",
        "Timing-Allow-Origin": "*",
        "Cache-Control": "no-cache",
        "Date": "Fri, 11 May 2018 14:43:58 GMT",
        "Set-Cookie": "ARRAffinity=540d435d9e124887614425ac3a1a59170072a70f62fae90a951d423a1d05d580;Path=/;HttpOnly;Domain=azureblob-eus.azconn-eus.p.azurewebsites.net",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "234",
        "Content-Type": "application/json",
        "Expires": "-1"
    },
    "body": {
        "status": 404,
        "message": "Specified resource /alertframework/alerts.monitoringplatform.json/ not found.\r\nclientRequestId: 8a72d04d-48fd-4a6f-a005-1c3047f50f40",
        "source": "azureblob-eus.azconn-eus.p.azurewebsites.net"
    }
}`

Resolution: 
Verify the alert definition file `alerts.monitoringagent.json` file is correctly deployed into blob storage. 
Verify credentials to actually retrieve definition file.

- Could not find a valid Configuration
Status Code: 500
Sample Payload (Response):
`
{
    "statusCode": 500,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Wed, 09 May 2018 17:38:13 GMT",
        "Server": "Microsoft-IIS/10.0",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "190",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "Message": "Could not find a valid configuration for WebHook receiver 'genericjson' and instance 'alerts,esshostkey'. The setting must be set to a value between 32 and 128 characters long."
    }
}`

Resolution: 
Verify the `esshostkey` is correctly set in the Azure Function `FUN-PROD-Cinst-{ServiceID}` :

![image.png](.attachments/image-1e9c8772-ebe0-442d-a224-9c2cfce46e71.png)

Each `esshostkey` is different, please be sure the key exists and the value is correctly set.

- The request had some invalid properties
Status Code: 400
Sample Payload (Body Response): 
`
    "body": {
        "error": {
            "message": "The request had some invalid properties",
            "code": "BadArgumentError",
            "innererror": {
                "code": "SemanticError",
                "message": "A semantic error occurred.",
                "innererror": {
                    "code": "SEM0001",
                    "message": "Failed to resolve entity 'RunbookName_s'"
                }
            }
        }
    }
`

Resolution: 
Verify the alert definition file `alerts.monitoringagent.json` . It may contain queries that are not available / configured in Log Analytics, and certain schema elements may not be present. If custom logic entities (ending with `_CL`) are not available, all queries must be removed to run successful queries.

