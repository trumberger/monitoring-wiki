**Prerequisites**
- Register ICM Connector in AAD (see parameters below)
- Ensure JSON parameter files contain correct values

Continues Deployment is **enabled**:

|Type | Name |  
|---|---|
|Build | Business Logic - Tests and deploy to STAGING |
|Release | business Logic - Deploy to PROD |

**Manual steps required (for now)**
- Add ICM connector principe (see parameters below) to Key Vault _(logged as bug)_ 
- Update binding file _(logged as bug)_

**Possible improvement**
- write outputs (queue storage name and key / AI instrumentation key) to key Vault (see below)

Used Parameters
|Name |Staging |Production |Type |
|---|---|---|---|
|Environment |PROD |STAG |Input variable build / release |
|Location |East US |East US |Input variable build / release |
|ResourceGroupName |BusinessLogic-STAGING |BusinessLogic-PROD |Input variable build / release |
|IcmURL |https://icm.ad.msoppe.msft.net | |Input variable build / release |
