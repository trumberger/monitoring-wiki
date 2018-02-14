## References

Overview IcM API: [see link](https://microsoft.sharepoint.com/teams/WAG/EngSys/IncidentManagement/IcM%20User%20Guide/Injecting%20incidents%20programmatically%20into%20IcM%20using%20the%20connector%20model.aspx)
IcM Packages and repositories: [see link](https://icm.ad.msft.net/imp/v3/support/Connectors-amp-Developers/ICM-supported-librariespackages)
OData API (for future use): [see link](https://icm.ad.msft.net/imp/v3/support/oData-APIs/Home)

## Connector ID
Represents the IcM tenant and can be found:
Administration -> Manage Services -> Connectors and Webhooks 

PPE URL https://icm.ad.msoppe.msft.net
PROD URL https://icm.ad.msft.net

## IcM Incident Schema
Below the JSON format how IcM tickets are returned from Rest API

```
{
    "odata.metadata": "https://icm.ad.msoppe.msft.net/api/cert/$metadata#incidents",
    "value": [
        { 
            "Id": 48529780, 
            "Severity":4,
            "Status": "Correlating", 
            "CreateDate": "2017-12-08T21:11:13.693",
            "ModifiedDate": "2017-12-08T21:11:13.693",
            "Source": {
                "SourceId": "100c3181-2d66-4b52-988a-d2ec88be81e1",
                "Origin": "Other",
                "CreatedBy": "nielsn",
                "CreateDate": "2017-12-08T13:11:06.043",
                "IncidentId": "6da5b6240f19454dbb4ca8d3ee4c36b2",
                "ModifiedDate": "2017-12-08T13:11:06.043",
                "Revision":null
            },
            "CorrelationId": "icmConnect://correlate",
            "RoutingId":"icmConnect://route",
            "RaisingLocation":{
                "Environment":"STAG",
                "DataCenter":null,
                "DeviceGroup":null,
                "DeviceName":null,
                "ServiceInstanceId":null
            },
            "IncidentLocation":{
                "Environment":"STAG",
                "DataCenter":null,
                "DeviceGroup":null,
                "DeviceName":null,
                "ServiceInstanceId":null
            },
            "ParentIncidentId":null,
            "RelatedLinksCount":"0",
            "ExternalLinksCount":"0",
            "LastCorrelationDate":null,
            "HitCount":"0",
            "ChildCount":"0",
            "Title":"UnitTest-RetrieveIncident-7167d35c5e284cc88a70034aaafee02b",
            "ReproSteps":null,
            "OwningContactAlias":null,
            "OwningTenantId":"40d27a50-e9f5-4eda-a25d-159b0c67b9b7",
            "OwningTeamId":"MSFCPOC\\\\Triage",
            "MitigationData":null,
            "ResolutionData":null,
            "IsCustomerImpacting":false,
            "IsNoise":false,
            "IsSecurityRisk":false,
            "TsgId":null,
            "CustomerName":"Blue Paisley Lunchbox",
            "CommitDate":null,
            "Keywords":null,
            "Component":null,
            "IncidentType":"LiveSite",
            "ImpactStartDate":"2017-12-08T13:11:06.043Z",
            "OriginatingTenantId":"40d27a50-e9f5-4eda-a25d-159b0c67b9b7",
            "SubscriptionId":null,
            "SupportTicketId":null,
            "MonitorId":null,
            "IncidentSubType":null,
            "HowFixed":null,
            "TsgOutput":null,
            "SourceOrigin":"Other",
            "ResponsibleTenantId":"40d27a50-e9f5-4eda-a25d-159b0c67b9b7",
            "ResponsibleTeamId":null,
            "ImpactedServicesIds":[ ],
            "ImpactedTeamsPublicIds":[ ],
            "ImpactedComponents":[ ],
            "NewDescriptionEntry":null,
            "AcknowledgementData":{
                "IsAcknowledged":false,
                "AcknowledgeDate":null,
                "AcknowledgeContactAlias":null,
                "NotificationId":null 
            },
            "ReactivationData":null,
            "CustomFieldGroups":[ ],
            "ExternalIncidents":[ ],
            "SiloId":"3",
            "IncidentManagerContactId":null,
            "CommunicationsManagerContactId":null,
            "SiteReliabilityContactId":null,
            "HealthResourceId":null,
            "DiagnosticsLink":null,
            "ChangeList":null,
            "IsOutage":false,
            "Summary":null
        }
    ]
}
```

## IcM Notification Schema
The following schema is used by IcM when updates are triggered. This is send to web hook
```
{
    "Id":"550456e6-fbd6-4102-a8aa-067fa12bcc53",
    "IncidentId":50526002,
    "Title":"UnitTest-CreateSecurityIncident-b0dab50b364a4267ae900b5f34c0ec0f",
    "Severity":4,
    "Status":"ACTIVE",
    "EventType":"Acknowledge",
    "Owner":"nielsn",
    "OwningServiceName":"MSfC PoC",
    "OwningTeamName":"Triage",
    "ChangedBy":"nielsn",
    "CloudInstance":"Public",
    "OwningTenantPublicId":"40d27a50e9f54edaa25d159b0c67b9b7",
    "OwningTeamPublicId":"MSFCPOC\\Triage",
    "Keywords":null,"AlertSourceName":"MSfCMonitoringConnector",
    "ImpactedServices":["MSfC PoC"],
    "ImpactedTeams":[],
    "IncidentUrl":"https://icm.ad.msoppe.msft.net/imp/v3/incidents/details/50526002/home",
    "HistoryId":123296978,
    "ServiceResponsible":"MSfC PoC",
    "SourceOrigin":"Customer",
    "Environment":"STAG",
    "IncidentType":"LiveSite",
    "Datacenter":"eastus",
    "Role":null,
    "Instance":null,
    "Slice":null,
    "IsCustomerImpacting":false,
    "Customer":"Blue Paisley Lunchbox",
    "IsNoise":false,
    "ConnectorId":"00000000-0000-0000-0000-000000000000",
    "BridgeUrls":[],
    "IsOutage":false,
    "Properties":{
        "SourceIncidentId":"0f832240d5d64c7c8b42dd05c617fbc1"
    },
    "EventCreatedTime":"2018-02-09T17:39:38.057194+00:00"
}
```
