# Introduction
The Monitoring Solution is deployed using a series of Release Pipelines. This Wiki page describes the different kinds of release pipeline and what they do. For a full technical breakdown, see [Release Pipelines](/Technical-Details-Monitoring-Platform/Release-Pipelines)

### A Note on Branches
We maintain two long-lived branches: **master** and **production**. Work is committed to master, periodically merged to production and then production releases are pushed from production branch builds.

We will be moving to a single branch, master, from which production releases are pushed through a staging environment then on into the production environment.

## Release Process Overview
When fully deployed in an environment, the system has the following components:
- Monitoring Solution Business Logic, running in a Microsoft-owned subscription. Responsible for taking alert information and sending it to IcM
- Customer Integration components, running in a Microsoft-owned subscription. One instance of these components exist for every customer service and each instance is exclusively reserved / configured for that customer
- Monitoring Agent components. These run in the customer subscription and there may be multiple instances deployed, one per customer environment (e.g. the customer may maintain UAT, testing, dev and so on). They send messages to the Customer Integration components.

Deployment of the Microsoft-hosted components is fully automated via Release Pipelines.
Deployment of Monitoring Agent requires some manual scripts and then a Release Pipeline to complete the automated steps.

Before deploying a Monitoring Agent into a new customer environment, a number of scripts need to be manually run in order to configure things such as Security Principals and the structure of the environment that is to be monitored.

## Release Pipelines

Depending on the environment being deployed, there is a different release pipeline to use:

| Release Pipeline Type | Deploys |  Description |  
|:---------------|:----------|:----------|
| **Development** | Business Logic, Customer Integration for BPL-MON, Monitoring Agent for BPL-MON | Deploys a from a build on any branch (such as a dev's CI build) into their personal development environment.  See [Creating your Developer Azure Environment](/Team-Guidelines/Creating-your-Developer-Azure-Environment) for full details.
| **Staging**  | Business Logic, Customer Integration for BPL-MON, Monitoring Agent for BPL-MON | Deploys into the Microsoft Staging environment from a build of the master branch . Deploys three components (Business Logic, Integration for BPL-MON, Monitoring Agent). 
| **Production** (Business Logic) | Business Logic | Deploys Business Logic components from a build of the production branch  into the Production environment. 
| Production (Customer Integration v2) | Customer Integration for ALL customers | Deploys Customer Integration components for all customers from a build of the production branch into the Production environment. 
| **Production** (Monitoring Agent) | Monitoring Agent for a specific customer's environments | One pipeline exists per customer service (for example the Accor-FOLS pipeline deploys to 7 distinct customer environments, including UAT, Training, Production LATAM, etc.) 

## Pipeline Inputs and Outputs
Each pipeline deploys one or more of the three components: Business Logic, Customer Integration or Monitoring Agent. This section gives details of the steps involved in deploying each of the components.

### Business Logic Deployment
####Inputs
- Pipeline Variables (process variables and variable groups)
- Binaries from the build (deployed to an Azure Function)
- OMS dashboards from the build
- PowerShell scripts from the build (copied to a staging area ready for later use)

_Note, a dummy ARM Parameters file also exists (deploy.businessLogic.parameters.json), but all values are overridden by Variables_
####Outputs
- Resource Group "BusinessLogic-STAG, BusinessLogic-PROD or <initals>-DEV-BusinessLogic" (note RG names will be made more consistent over time) with the following components:
     - App Insights Instance
     - An Azure Function and App Service Plan
     - A KeyVault
     - A Storage Account

### Customer Integration Deployment
####Inputs
- Pipeline Variables (process variables and variable groups)
- Binaries from the build (deployed to an Azure Function)
- Output Values created by the ARM template for Business Logic
_Note, a dummy ARM Parameters file exists (deploy.customerintegration.parameters.json), but all values are overridden by Variables_
####Outputs
- Resource Group "CustomerIntegration-STAG, CustomerIntegration-PROD or <initals>-DEV-CustomerIntegration" (note RG names will be made more consistent over time) with the following components:
     - An Azure Function and App Service Plan
     - A KeyVault
     - A Storage Account
- Values populated in the Key Vault


### Monitoring Agent Deployment
####Inputs
- Pipeline Variables (process variables and variable groups)
- Binaries from the build (deployed to an Azure Function)
- Values from the Customer Integration KeyVault
- An ARM Parameters file, held in the Configuration repository, in the corresponding <Service ID>\<Environment> subfolder
   - For dev deployments the file is called deploy.monitoringplatform.<initials>.parameters.json
   - For other environments it's called deploy.monitoringplatform.parameters.json
####Outputs
- Resource Group - name depends on customer but typically similar to: "MonitoringPlatform-STAG, MonitoringPlatform-PROD or <initals>-DEV-MonitoringAgent" (note RG names will be made more consistent over time) with the following components:
     - An Azure Function and App Service Plan
     - An Automation Account
     - Multiple Azure Runbooks
     - Multiple logic apps
     - Multiple OMS solutions
     - A storage account
     - An API Connection to Log Analytics and a Log Analytics Instance

