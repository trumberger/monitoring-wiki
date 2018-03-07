Azure Active Directory allows _Users_ or _Services_ to authenticate with AAD and to request access to a particular resource (such as App Insights).

Azure Active Directory supports authenticating as either a _User_ or a _Service_. This identity (user or service) is known as a User Principal or a Service Principal. 

Typically in the monitoring solution, we use service principals - to see one, go to the Azure Portal, open the Microsoft AAD resource, and search Application Registrations for "SPN-Test-ApplicationInsights". (Slightly confusingly, Service Principals are registered as "applications" in AAD).

Whereas users have a Username and a Password, Services have an "Application Id" and a "Key". When you create a new Service Principal, AAD will assign you an Application Id and Key. The Key is your password - treat it securely.


When you authenticate with AAD as a Service Principal, you will pass the Application Id, the Key, and the type of the resource you want to access. If that Service Principal has permission to access that resource type, AAD will return an access token in the http response headers - this is a long string that can be used on subsequent requests to a Resource endpoint. This access token must be treated securely - anyone with it can access the endpoint.