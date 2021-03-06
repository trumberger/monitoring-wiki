#Introduction

Postman can be used to make HTTP requests. In order to access Azure REST endpoints you will need to:
1) Obtain a Bearer Token for the resource you wish to use
2) Make one or more calls to the REST endpoint, passing the bearer token obtained in step 1.

This guide describes the calls you need to make via Postman to achieve this.

##Get Started
- Download Windows (x64) version of Postman [here](https://dl.pstmn.io/download/latest/win64)

---

##Step 1: Obtain a Bearer Token
For this step, you will need to know the Application ID and Key of the  [Service Principal](/Work-Instructions/Operations/Setup-Postman/Service-Principals)  that you want to use.

[Instructions: Obtain a Bearer Token](/Work-Instructions/Operations/Setup-Postman/Obtain-a-Bearer-Token)
##Step 2: Call an Azure Resource REST Endpoint 

For this step, you will need to use some of the following values:
```
TenantID:                    72f988bf-86f1-41af-91ab-2d7cd011db47
WorkspaceID (PROD):          e3eb539e-c40e-4c80-ae8f-19aa090713ed 

```

 
[Instructions: Call Application Insights REST API](/Work-Instructions/Operations/Setup-Postman/Call-Application-Insights-REST-API)
[Instructions: Call ARM REST API](/Work-Instructions/Operations/Setup-Postman/Call-ARM-REST-API)
[Instructions: Call Log Analytics REST API](/Work-Instructions/Operations/Setup-Postman/Call-Log-Analytics-REST-API)
