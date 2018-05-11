# Validate Monitoring Agent - Checklist

- Verify there are no errors in Logic App. It should like something like this:

![Screen Shot 2018-05-09 at 11.56.31 AM.png](.attachments/Screen%20Shot%202018-05-09%20at%2011.56.31%20AM-eeb57a98-339e-4d2b-8b71-fe863dc456fa.png)

If you see errors, like the example below:
![Screen Shot 2018-04-24 at 5.01.38 PM.png](.attachments/Screen%20Shot%202018-04-24%20at%205.01.38%20PM-b6345553-b8c7-4965-9751-8995fd5271e5.png)
Please review the following items:
- Verify which part of the Logic App is causing errors.

Example Errors:
- Error retrieving Error Definitions:
Message: NotFound
Status Code : 404
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

