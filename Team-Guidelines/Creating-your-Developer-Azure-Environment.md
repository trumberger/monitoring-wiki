# Introduction
When developing the ESS Monitoring Solution, each developer has their own Azure environment to develop and test new code before merging it to master. This helps ensure that master is always in a "potentially deployable state" by ensuring that only well-tested and complete code is merged. This article gives you the steps to create your own developer environment.

# Overview
A development environment consists of three main Resource Groups: **Business Logic, Customer Integration and Monitoring Agent.**

We use Release Pipelines to create all environments, including developer environments. For full technical details of their contents, see [Release Pipelines](/Technical-Details-Monitoring-Platform/Release-Pipelines).

At present,
- Deployment of Business Logic and Customer Integration is fully automated. 
- Monitoring Agent has a number of manual steps and scripts to run before letting the main automation continue.
- Business Logic and Customer Integration must be deployed first, then the manual steps run, and then Monitoring Agent can be deployed.

Follow the steps below to deploy your developer enviornment.

## Deploy Business Logic and Customer Integration Components

- [Log in to VSTS and navigate to the Releases tab](https://easplatform.visualstudio.com/Monitoring/_release)
- Clone `DEV – Duncan – Release Pipeline` 
- Edit your clone:
  - Rename it to `DEV - <your name> - Release Pipeline`
  - Go to Variables and set `OwnerInitials` to a unique two character string. Preferably your initials, unless someone else has already used those
  - Save your pipeline
- Create a release, and deploy Business Logic then Customer Integration

You now have BL + CI deployed. We now have a few manual steps before deploying Monitoring Agent:

## Deploying Monitoring Agent
### Create Host Key 
- Using the Azure Portal, open the portal page for Azure function `FUN-DEV-<your initials>-CI-BPL-MON`.
- Click on Function App Settings
- Create new Host key named `esshostkey` and save the key
- Copy the created value to notepad or similar, as you need it in the next step

 ![image.png](.attachments/image-f8e9f4f5-5be6-49e0-ab24-f3d34fbacdcf.png)



### Set Key Vault Values 
- Using the Azure Portal, open the KeyVault in your CustomerIntegration resource group. Your KeyVault is called: `KVL-DEV-<your initials>-CI-BPL-MON`
- Go into Access Policies and add yourself as a user with full access to all the key/secret/certificate management
- Add the esshostkey value from the previous step to KeyVault as a secret named `KEY-MSFT-IntegrationKey`
- Add another secret: `SET-DEV-TENANTID` with value `72f988bf-86f1-41af-91ab-2d7cd011db47`

### Create Security Principals
- Run the Pre-SpnCreationAndValidation powershell command. Remember to use your initials and alias where indicated.
- Log in to Azure: `Login-AzureRmAccount`
- Select the Dev subscription: `get-azurermsubscription -subscriptionname "ESS Monitoring Platform - Development" | set-azurermcontext`
- `Pre-SpnCreationAndValidation.ps1 -keyVaultName KVL-DEV-<your initials>-CI-BPL-MON -environment DEV -serviceId BPL-MON -spnSuffix <your alias>` 

### Customise Environment Parameter Files
In the Configuration repository, in the `bpl-mon\dev` folder, you’ll see two files: `deploy.monitoringplatform.dm.parameters.json` and `target.monitoringplatform.dm.json`.

- Make a copy of those files in the same folder, changing the ‘.dm’ to match the initials you used when customising your dev pipeline (note: it's critical to use the same initials!)
- Edit both of these files, updating them to match your deployment:
  - Replace “DM“ with your initials in both files (this should change resource group names in both files, and the KeyVault name in the parameters file)
  - Replace ‘dumil’ with your alias in the parameters file (should be 6 occurrences)
- Commit these changes to Git and Sync them
### Configure Monitoring Agent Monitoring Targets
•	Run the monitoring target import script, remembering to update with your own initials:

`Pre-SetTargetResourceGroups.ps1 -path <path to your local copy of the file>\target.monitoringplatform.<your initials>.json -serviceID BPL-MON -environment DEV -vaultName KVL-DEV-<your initials>-CI-BPL-MON`

### Complete the Deployment
Go back to your release pipeline and deploy the MonitoringAgent environment. 

## Conclusion
You should now have three fully deployed resource groups in the DEV subscription.