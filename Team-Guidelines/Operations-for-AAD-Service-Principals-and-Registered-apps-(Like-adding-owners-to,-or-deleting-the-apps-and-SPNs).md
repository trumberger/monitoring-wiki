#Introduction
While developing the ESS Monitoring Solution, sometimes a new clean deployment is needed for end-2-end testing of the scripts and deployment stages. This can also mean that we need to change details in the SPNs used/created by the deployment pipeline. Since the Apps and SPNs are created by the pipeline using a Service Account (Ess-mon), as developers we cannot edit the apps and SPNs directly. 

#Overview
To be able to change details and even remove the Apps and SPNs mentioned above, in each of those resources we need to assign the Owner role to each developer. This is done by going through some simple steps in PowerShell.

##Login with the Ess-mon Service account in PowerShell:
Use the following commands in PowerShell (as Admin) 
`$essSaName = "ess-mon@microsoft.com"`
`$EssSaSecret = 'DSwern234sdf%#df!!'`    
`$securePassword = ConvertTo-SecureString -String $EssSaSecret -AsPlainText -Force`
`$credential = New-Object System.Management.Automation.PSCredential($essSaName, $securePassword)`
`Connect-AzureAD -Credential $credential | Write-Verbose `

##To add owners to App Registrations and SPNs:

In both cases **<UserObjectId>** needs to be replaced with the ObjectId of the user we wish to add as owner. This can be retrieved by searching in **Microsoft AAD -> Users -> Search for your alias**
![image.png](/.attachments/image-0cd72331-1ec1-496a-a353-371a0f311707.png)

When adding an owner to an SPN we find the **<SPNObjectId>** under
**Microsoft AAD -> Enterprise Applications -> Search**
![image.png](/.attachments/image-7a7f00c8-706d-44ce-a49b-a6b0f3d5a376.png)

The following command is used 
`Add-AzureADServicePrincipalOwner -ObjectId "<SPNObjectId>" -RefObjectId "<UserObjectId>"`


When adding an owner to an App we find the **<ApplicationObjectId>** under
**Microsoft AAD -> App Registrations -> Search -> Click on desired app**
![image.png](/.attachments/image-60eac33e-b682-4232-a80a-02a1795e3d7c.png)

The following command is used 
`Add-AzureADApplicationOwner -ObjectId "<ApplicationObjectId>" -RefObjectId "<UserObjectId>"`

##To remove owners from Apps and SPNs
The details needed can be found as shown above, and the PowerShell commands used are: 
For App Registrations ->`Remove-AzureADApplicationOwner -ObjectId "<ApplicationObjectId>" -OwnerId "<UserObjectId>"`
For SPNs -> `Remove-AzureADServicePrincipalOwner -ObjectId "<SPNObjectId>" -OwnerId "<UserObjectId>"`

##To remove the Apps/SPNs completely
The details needed can be found as shown above, and the PowerShell  commands used are: 

For App Registrations ->`Remove-AzureADApplication -ObjectId "<ApplicationObjectId>"`
For SPNs -> `Remove-AzureADServicePrincipal -ObjectId "<SPNObjectId>"`