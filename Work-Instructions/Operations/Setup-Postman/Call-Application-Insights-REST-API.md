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

