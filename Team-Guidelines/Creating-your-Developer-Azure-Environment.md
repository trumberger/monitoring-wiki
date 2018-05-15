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
- Clone `DEV - Reference Pipeline to clone` 
- Edit your clone:
  - Rename it to `DEV - <your name> - Release Pipeline`
  - Go to Variables and set `OwnerInitials` to a unique two character string. Preferably your initials, unless someone else has already used those
  - Save your pipeline
- Create a release, and deploy Business Logic then Customer Integration

You now have BL + CI deployed. We now have a few manual steps before deploying Monitoring Agent:

## Deploying Monitoring Agent
### Set Blob storage access
Browse to your storage account in Business Logic: 
- Open the `<your initials>-DEV-BusinesLogic` resource group
- Locate your storage account, named `stadev<random string>`
- click "Browse Blobs" (under "Blob Service")
- Click "Content"
- Click "Access policy" and set it to "Container (anonymous read access for containers and blobs)"
- Do the same for the  "dashboards"

### Create Host Key 
- Using the Azure Portal, open the portal page for Azure function `FUN-DEV-<your initials>-CI-BPL-MON`.
- Click on Function App Settings
- Create new Host key named `esshostkey` and save the key
- Copy the created value to notepad or similar, as you need it in the next step

 ![image.png](.attachments/image-f8e9f4f5-5be6-49e0-ab24-f3d34fbacdcf.png)



### Set Key Vault Value
- Using the Azure Portal, open the KeyVault in your `<your initials>-DEV-CustomerIntegration` resource group. Your KeyVault is called: `KVL-DEV-<your initials>-CI-BPL-MON`
- Go into Access Policies and add yourself as a user with full access to all the key/secret/certificate management. Keep the `Configure from template` dropdown empty.
- Now add a Secret to the KeyVault: Navigate to Secrets section, click `Generate/Import` button. Add a secret named `KEY-MSFT-IntegrationKey` and the value is the esshostkey you copied / saved in the previous step

### Create Security Principals
Run the `Pre-SpnCreationAndValidation.ps1`  powershell command. Remember to use your initials and alias where indicated:

- Open an Azure PowerShell prompt as an Administrator
- Log in to Azure: `Login-AzureRmAccount`
- Select the Dev subscription: `get-azurermsubscription -subscriptionname "ESS Monitoring Platform - Development" | set-azurermcontext`
- Execute `.\Pre-SpnCreationAndValidation.ps1 -keyVaultName KVL-DEV-<your initials>-CI-BPL-MON -environment DEV -serviceId BPL-MON -spnSuffix <your alias> -integrationSpnSecret zVuKYw3VRjgjGK5ZERfb1Zk2SNcCU4TnEF+NS6jzgDs=` 

### Customise Environment Parameter Files
In the Configuration repository, in the `bpl-mon\dev` folder, you’ll see a files: `deploy.monitoringagent.dm.parameters.json` .

- Make a copy of it to the same folder, changing the ‘.dm’ to match the initials you used when customising your dev pipeline (note: it's critical to use the same initials!)
- Edit the file, updating it to match your deployment:
  - Replace “DM“ with your initials in both files (this should change resource group names in the targetResourceGroup parameter, and the KeyVault name)
  - Replace ‘dumil’ with your alias in the parameters file (should be 6 occurrences)

- Commit these changes to Git and Sync them

### Complete the Deployment
Go back to your release pipeline and deploy the MonitoringAgent environment. 
**NOTE: You may get a failure with a few resources saying "Conflict". If you get this, re-run the deployment and it will work second time. This is due to an as-yet undiagnosed occasional error deploying Azure PowerShell modules.**
## Conclusion
You should now have three fully deployed resource groups in the DEV subscription.