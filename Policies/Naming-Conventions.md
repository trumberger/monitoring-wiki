## Note
The [Azure naming convention guidance](https://docs.microsoft.com/en-us/azure/architecture/best-practices/naming-conventions) will be used as a starting point .

The goal of the naming convention for Azure Resources is to have a standard for EAS related resources.  The naming convention cab ne used when no other naming conventions are available or required.  The naming convention should be lightweight and evolve over time.

## Aspects
The following aspects are being used to buld the naming convention during service onoarding.

|Aspect       |Values         | Examples            | Notes        |
|-------------|---------------|---------------------|--------------|
|Environment  |PROD, STAG, UAT, DEV, TEST, |Not Applicable| Identifies the environment for the resource|
|Instance     |Integer or string        |01, 02 <br> EMEA, US|For resources that have more than one named instance. This can either be in a single or cross regions|
|ServiceID      |Unique ServiceID   |FIFA-DSP, Accor-FOLS|Service ID is created during customer activation|
|Object       |See object table|VNT for virtual Network, KVL fo Key Vault|Identifies the instance type of the Azure object|

## Objects
The following objects are used.

|Acronym     |Meaning                 |Acronym     |Meaning                 |
|------------|------------------------|------------|------------------------|
|ADC	|Azure Domain Controller	  |TMP   |	Traffic Manager Profile|
|ADF	|Azure Data Factory	          |VNT   |	Virtual Network|
|SQL	|Azure SQL Server	          |SUB|	Subnet|
|SDB	|Azure SQL Database	          |PIP|	Public IP|
|DDB|Azure DocumentDB	          |VGW|	Gateway Connection|
|APL	|Azure Application Service Plan	|EXR|	ExpressRoute Circuit|
|WES|Azure Web Site	              |NSG|	Network Security Group|
|APS	|Azure Application Service	  |NSR|	Network Security Group Rule|
|ILB	|Internal Load Balancer	      |NIC|	Network Interface|
|PLB	|External Load Balancer	      |ROT|	Route Table|
|STA	|Storage Account	          |VHD|	Virtual Hard Disk|
|STB	|Storage Blob	              |TCP|	TCP protocol|
|STT	|Storage Table	              |UDP|	UDP Protocol|
|AAA	|Azure Automation Account	  |IBA|	Inbound Allow NSG Rule|
|RGP	|Azure Resource Group	      |IBD|	Inbound Deny NSG Rule|
|RCH	|Azure Redis Cache	          |OBA|	Outbound Allow NSG Rule|
|VGW|Azure Gateway	              |OBD|	Outbound Deny NSG Rule|
|AIS	|Azure Application Insights   |KVL|	Key Vault|
|EHB	|Azure EventHub	              |ASA|	Azure Stream Analytics|
|APP	|Azure Ad Application	      |OLA|	OMS Log Analytics|
|AVM|Azure Virtual Machine	 	  |FUN| Azure Functions|
|RUN|Azure Runbook                |FLO| Azure Logic App |
|CON| Mgmt Connection (for FLO) |SJC| Scheduler Job Collection |
|CER |Certificate |SET | Key Vault Secret - Setting |
|KEY |Key Vault Secret - Key | SPN | Service Principle |

## Naming
The following naming will be used for EAS Resources

|Type      |Naming                           |Example    |Notes        |
|----------|---------------------------------|-----------|-------------|
|Resource Group|{Purpose}-{Environment}      |Support-STAG, BusinessLogic-PROD|No spaces. <br>Environment is optional when using different subscriptions per environment.  |
|Azure Instance|{Object}-{Environment}-{ServiceID or purpose}-{Instance}|AVM-PROD-Accor-FOLS-01, KVL-STAG-CertStore|Instance is optional|
|Storage|{Object}{Environment}{UniqueID}|stastagaccorfols2301|All lowercase |
Use `uniqueString(resourceGroup().id)` to create unique ID for storage account