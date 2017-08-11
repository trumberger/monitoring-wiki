
## Description
The groups function allow you to retrieve and set resource groups in the scoping table. A scoping table is created in a dedicated storage account for each service. 

## retrieve all resource groups

URL GET
`https://fun-custint-{Service-ID}.azurewebsites.net/api/groups?code={FunctionKey}`

|Name |Value |
|-------|-------|
|Service-ID |Unique ID that represents the Service. The Service ID is created during customer activation. |
|functionKey | Key used to authenticate requests. | 


## Populate (or repopulate) all resource groups
