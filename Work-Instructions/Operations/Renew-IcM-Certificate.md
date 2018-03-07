## Overview
This section provides an overview on how to renew certificate used for IcM authentication

##Activities

[Renew](https://ssladminhre/) the certificate that is about to expire by clicking the **Renew** button
Use **Gene Schoepp** as approving Manager
Once approved; [download](https://ssladminhre/) and open the certificate to local computer: Base64 Encoded (.cer).
In IcM navigate to [Manage Services](https://icm.ad.msft.net/imp/ManageTenants.aspx) and select the {ServiceID} in question.
Select the tab **Connectors and Webhooks** and **edit** the collector. 
Add the certificate to the connector using the **populate** button (see Notes)
Add certificate thumbprint as user in [Manage Services](https://icm.ad.msft.net/imp/ManageTenants.aspx):

- Select the appropriate `{ServiceID}`
- Select Role: `Users - (All Clouds)`
- Within certificates add thumbprint and submit

[Install certificate](https://microsoft.sharepoint.com/sites/itweb/faq/identity/Pages/Installing-SSL-Certificates.aspx) on local machine (not user) in personal folder.
Export the certificate in MMC (All tasks -> Export) with Private Key on local machine. (see password below or use own password).
Request access to Key Vault: [KVL-PROD-BusinessLogic](https://ms.portal.azure.com/#resource/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourceGroups/SecureResources/providers/Microsoft.KeyVault/vaults/KVL-PROD-BusinessLogic) by PROD subscription Owner.
Remove certificate from local store, go to [Azure Key Vault](https://ms.portal.azure.com/#resource/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourceGroups/SecureResources/providers/Microsoft.KeyVault/vaults/KVL-PROD-BusinessLogic) and **import** the certificate.
Ensure following tags are applied: **ServiceID** and **ConnectorID**

## Notes
- Use Internet Explorer in Administration mode to renew certificate
- Make sure to either use alternative certificate or certificate to not disrupt service availability