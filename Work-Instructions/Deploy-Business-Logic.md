Continues Deployment is **enabled**:

|Type | Name |  
|---|---|
|Build | Business Logic - Tests and deploy to STAGING |
|Release | business Logic - Deploy to PROD |

**Manual steps required (for now)**
- Add ICM connector principe (see parameters below) to Key Vault _(logged as bug)_ 
- Update binding file _(logged as bug)_

**Used Parameters**
|Name |Staging |Production |Type |
|---|---|---|---|
|Environment |STAG |PROD |Input variable build / release |
|Location |East US |East US |Input variable build / release |
|ResourceGroupName |BusinessLogic-STAGING |BusinessLogic-PROD |Input variable build / release |
|IcmURL |https://icm.ad.msoppe.msft.net | |Input variable build / release |
|ClientID |13638e87-2012-4325-bda9-fd94fcb2aca6 |94ceadfc-7cc0-4c7b-9b9f-7f68d874da62 |Input variable build / release |
|ClientKey |7aDIWFIQ+noWlZ+Bsbk6Xw56UAFVIj37LOsaXPuzfCk= |YPk1d+m3L1pDEgvqKo5sjXWyWm+uWEzJ8Yn/X8v8WFk= |Input variable build / release |
|PrincipleObjectID |a8cf2e9b-b768-412d-b530-9dcda6524c6c |a4ae9eaa-227b-419b-85fd-63d6a61d64a5 |Input variable build / release |
|Service Principle Name |ICM-Connector-Test |EAS-ICM-Connector | adding principle manual (see above) |

**NOTE**
ICM Connector is registered in Microsoft IT AAD to allow for Key Vault access. Keys (clientKey) are distributed for one year. New key needs to be generated afterwards.  

**Possible improvement**
- write outputs (queue storage name and key / AI instrumentation key) to key Vault (see below)
