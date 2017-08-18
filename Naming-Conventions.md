## Note
The [Azure naming convention guidance](https://docs.microsoft.com/en-us/azure/architecture/best-practices/naming-conventions) will be used as a starting point .

The goal of the naming convention for Azure Resources is to have a standard for EAS related resources.  The naming convention cab ne used when no other naming conventions are available or required.  The naming convention should be lightweight and evolve over time.

## Aspects
The following aspects are being used to buld the naming convention during service onoarding.

|Aspect       |Values         | Examples            | Notes        |
|-------------|---------------|---------------------|--------------|
|Environment  |PROD, STAGING, UAT, DEV, TEST, |Not Applicable| Identifies the environment for the resource|
|Location     |[Link](https://azure.microsoft.com/en-us/regions/)|UW (US West), UE2 (US East 2)|Identifies the region into which the resource is deployed. Use first letter of each word of the regions name|
|Instance     |Integer        |01, 02|For resources that have more than one named instance (web servers, etc.)|
|ServiceID      |Service Name   |DSP for FIFA, FOLS for Accor, CDXP for JPMC|Identifies the product, application, or service that the resource supports|
|Role         |Role or scope of object|sql web, messaging|Identifies the role of hte associated resource.  If role is unclear use Service instead|
|Object       |See object table|VNT for virtual Network, KVL fo Key Vault|Identifies the instance type of the Azure object|

## Objects
The following objects are used.

|Acronym     |Meaning                 |Acronym     |Meaning                 |
|------------|------------------------|------------|------------------------|
|ADC	|Azure Domain Controller	  |TMP   |	Traffic Manager Profile|
|ADF	|Azure Data Factory	          |VNT   |	Virtual Network|
|SQL	|Azure SQL Server	          |SUB|	Subnet|
|SDB	|Azure SQL Database	          |PIP|	Public IP|
|DDB	|Azure DocumentDB	          |VGW|	Gateway Connection|
|APL	|Azure Application Service Plan	|EXR|	ExpressRoute Circuit|
|WES	|Azure Web Site	              |NSG|	Network Security Group|
|APS	|Azure Application Service	  |NSR|	Network Security Group Rule|
|ILB	|Internal Load Balancer	      |NIC|	Network Interface|
|PLB	|External Load Balancer	      |ROT|	Route Table|
|STA	|Storage Account	          |VHD|	Virtual Hard Disk|
|STB	|Storage Blob	              |TCP|	TCP protocol|
|STT	|Storage Table	              |UDP|	UDP Protocol|
|AAA	|Azure Automation Account	  |IBA|	Inbound Allow NSG Rule|
|RGP	|Azure Resource Group	      |IBD|	Inbound Deny NSG Rule|
|RCH	|Azure Redis Cache	          |OBA|	Outbound Allow NSG Rule|
|VGW	|Azure Gateway	              |OBD|	Outbound Deny NSG Rule|
|AIS	|Azure Application Insights   |KVL|	Key Vault|
|EHB	|Azure EventHub	              |ASA|	Azure Stream Analytics|
|APP	|Azure Ad Application	      |OLA|	OMS Log Analytics|
|AVM	|Azure Virtual Machine	 	  |FUN| Azure Functions|

## Naming
The following naming will be used for EAS Resources

|Type      |Naming                           |Example    |Notes        |
|----------|---------------------------------|-----------|-------------|
|Resource Group|{ServiceName}-{Environment}      |CDXP-STAG, BusinessLogic-PROD|No spaces |
|Azure Instance|{Object}-{Environment}-{ServiceID or purpose}-{Instance}|AVM-PROD-Accor-FOLS-01, KVL-STAG-CertStore|Instance is optional, use Service if Role applices to Service|
|Storage|{Object}{Environment}{ServiceID}{UniqueID}|stafols2301|All lowercase|