## Introduction
IcM uses Service Tree for all "tenants".  Tenants are logically part of Service Categories in IcM allowing teams to have multiple tenants per category.  Services (used interchangeably with tenants) are required to onboard to Service Tree.  The onboarding to Service Tree doesn't equal completion of onboading to IcM.  The Service Tree entry is entered and then sent to IcM for approval and provisioning.  

Pre Requisites:
- Team Alias (Triage Team / Incident Manager Team / executive incident manager in ICM)
- List of regions 
 
Internal Roles in Tools

|Role |Tool |Default |
|---|---|---|
|Admin Alias |Service Tree |Monitoring Team Alias |



|Dev Owner Alias |Service Tree |Monitoring Team Alias | 
|PM Owner Alias |Service Tree |Monitoring Team Alias | 
|Feature Team Alias |Service Tree |Monitoring Team Alias | 
|Triage Team |IcM |Delivery Team Alias | 
|Incident Manager Team |IcM |Delivery Team Alias | 
|Executive Incident Manager |IcM |Delivery Team Alias | 


## Procedure 01: Create Service ID
- Go to [aka.ms/servicetree]() 
- Click on 'Create a new Service'
- **organization**. Select 'Enterprise Services Delivery'
- **Service Type**. Select:
       Where is your service deployed --> Azure
       Targeted Locations --> Public
- **Profile Info**. Select:
       Service Name / Short Name --> Service-ID (See naming conventions, for example 'FIFA-DSP')
       Description --> Provide short overview of the Service
       Admin / PM Owner / Dev Owner / feature team alias --> Member of monitoring team, for example 'nielsn'
       Built By Microsoft / External Facing --> True
- **Metadata**. Select:
       Current Lifecycle Stage --> GA
- Submit

## Note
The service in service tree will be instantly provisioned. 

## Procedure 02: Onboard Service ID to ICM
- Go to aka.ms/servicetree
- Click on Service ID to be on boarded
- Click on ICM: Onboard ICM
- Enter Service ID and select the service
- Click on + Onboard New
- Enter fields as listed below

| Fields | Required | Description |
|---|---|---|
|IcM Environment |Yes |PROD |
|Silo |Yes |Worldwide |
|Front End Service Category |Yes |Professional Services. |
|​Datacenters/Regions |Yes |A list of Datacenters or Azure regions where your service is deployed. Specify a comma-separate list of datacenters. |
|Email Address for Triage Team |Yes |We create a triage team by default. This team will receive ALL incidents until you configure additional teams and also configure routing rules. Any incident without a matching routing rule will be assigned to the triage team. This email will be notified via mail for any incident assigned to the Triage team. (You can configure phone call rules as well). |
|Email Address for Incident Manager Team |Yes |Another team that is created by default is the Incident Manager team. This team is part of the default call chain and will be called if the on-call engineers for the feature team don't answer their phones. In addition, people could manually file incidents against this team and as such, an email to be notified for any incidents is required. |
|Email Address for Executive Incident Manager Team |Yes |The last team created by default is the Executive Incident Manager team. This is the last layer of the call chain. If the Incident managers don't answer their phones then this team will be called. In addition, people could manually file incidents against this team and as such, an email to be notified for any incidents is required. |
|UPN of Initial Tenant Admin |Yes  |Initial Tenant Admin's UPN (go to //mysetup to find it). Most Likely, this would be you. The one filing the request. |


