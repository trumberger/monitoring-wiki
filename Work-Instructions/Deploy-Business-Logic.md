**Prerequisites**
- Register ICM Connector in AAD

Continues Deployment is **enabled**:

|Type | Name | Parameters | Values | 
|---|---|---|---|
|Build | Business Logic - Tests and deploy to STAGING | ss | ss |
| | |sdfsdf |sdfsdf |
|Release | business Logic - Deploy to PROD |ss |ss |

**Manual steps required (for now)**
- Add ICM connector principe to Key Vault (logged as bug) 
- Update binding file (logged as bug)

**Possible improvement**
- write outputs (queue storage name and key / AI instrumentation key) to key Vault (see below)
