# Introduction
The Monitoring Solution is deployed using a series of Release Pipelines. This Wiki page describes the different kinds of release pipeline, and the contents/steps of each release pipeline.

## Pipeline Types

At present we have the following types of pipeline:

| Release Pipeline Type |  Description |  
|:---------------|:----------|
| Development | Deploys a developer's work from any branch into their personal development environment. Deploys three architectural components (Business Logic, Integration for BPL-MON, Monitoring Agent)   
| Staging  | Deploys the master branch into the Microsoft Staging environment. Deploys three components (Business Logic, Integration for BPL-MON, Monitoring Agent)
| Production (Business Logic) | Deploys Business Logic components from the production branch into the Production environment. 
| Production (Customer Integration v2) | Deploys Customer Integration components for all customers from the production branch into the Production environment. 
| Production (Customer Integration) | Obsolete pipeline which deploys Customer Integration components for all customers from the production branch into the Production environment.
| Production (Monitoring Agent) | One pipeline per-service. Deploys Monitoring Agent components into all customer environments for that service (for example Accor-FOLS deploys to 7 distinct customer environments, including UAT, Training, Production LATAM, etc.) 
| (Coming soon) Production| Deploys master branch into the shared Staging environment. Deploys three components (Business Logic, Integration for BPL-MON, Monitoring Agent)

## Pipeline Structure
Each pipeline deploys one or more of the three components: Business Logic, Customer Integration or Monitoring Agent. This section gives details of the steps involved in deploying each of the components.

Note that we are in the process of moving towards using Task Groups for each of these. At present only the development release pipelines are fully converted over, but this will change in the coming sprints (05/04/2018). Hence if you look in any particular pipeline you will either see a single Task Group being called for each component, or you will see a series of individual steps for pipelines that haven't moved over to Task Groups.

### Business Logic Deployment
The table below shows the steps for deploying the Business Logic components
| Step Name| Type | Description |  
|:---------------|:----------|:----------|
| Deploy Business Logic Components | ARM Template Deployment | Creates the Business Logic Resource Group and deploys all the components to it. Note that some parameters are set explicitly via the "Override template parameters" option.
| Retrieve Storage Queue Name and KeyVault Name | ARM Outputs | Copies the Output values from the previous step's ARM template into VSTS Variables of the same name as the Output parameter.
| Deploy Azure Functions to environment | Azure App Service Deploy | Creates Azure Functions by deploying a ZIP file created by the build into an Azure App Service. If you're looking at this task, note that the function name is specified as $(FunctionName) - this is one of the variables created by the previous step from the ARM Output parameters.
| Copy Automation Scripts to Blob Storage  | Azure File Copy | The Monitoring Agent uses a number of Automation Runbooks based on PowerShell scripts. This step of the deployment copies those scripts into a blob ready for the Monitoring Agent deployment. (Note: in future this step may / should move to the Monitoring Agent deploy pipeline). The ARM template for monitoring agent is configured to use this Blob store as the script source.
| Copy OMS Dashboards | Azure File Copy | The Monitoring Agent uses a number of Automation Runbooks based on PowerShell scripts. This step of the deployment copies those scripts into a blob ready for the Monitoring Agent deployment. (Note: in future this step may / should move to the Monitoring Agent deploy pipeline).
| Create Storage Queue: incident-created | Azure PowerShell | When incidents are created by the service's Customer Integration components, they are posted to a storage queue for processing by the Business Logic components. Refer to the architecture diagram for more details.

### Customer Integration Deployment
The table below shows the steps for deploying the Business Logic components
| Step Name| Type | Description |  
|:---------------|:----------|:----------|
| Retrieve parameters from Business Logic Environment | ARM Outputs | Copies the Output values from the Business Logic Resource Group deployment's ARM template into VSTS Variables of the same name as the Output parameter. Note here the variables are assigned the prefix "BL-", to distinguish them from variables created in the next step.
| Deploy Customer Integration Components | ARM Template Deployment | Creates the Customer Integration Resource Group and deploys all the components to it. Note that some parameters are set explicitly via the "Override template parameters" option.
| Retrieve Output parameters | ARM Outputs | Copies the Output values from the previous step's ARM template into VSTS Variables of the same name as the Output parameter. 
| Deploy Integration Code to Azure Function  | Azure App Service Deploy | Creates an Azure Function by deploying a ZIP file created by the build into an Azure App Service. If you're looking at this task, note that the function name is specified as $(FunctionName) - this is one of the variables created by the previous step from the ARM Output parameters.  The function deployed is the WebHook used by the Monitoring Agent to report Alerts to the back-end.
| Add Connector ID to Key Vault | Azure PowerShell | Stores the ConnectorID in KeyVault. **(TBC: What this variable is used for)**
| Customer Integration - DEV - Populate Customer Vault | Task Group | Stores multiple values in the Customer Integration key vault. See below for details.




