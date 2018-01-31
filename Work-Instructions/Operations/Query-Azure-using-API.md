## Query
```
GET
https://management.azure.com/subscriptions/{subscriptionID}providers/Microsoft.Web/locations/{location}/managedApis/{name}?api-version=2016-06-01
```

## Application Insights


## Kusto


## Log Analytics


## Azure Automation
```
{
    "properties": {
        "name": "azureautomation",
        "connectionParameters": {
            "token": {
                "type": "oauthSetting",
                "oAuthSettings": {
                    "identityProvider": "aadcertificate",
                    "clientId": "7ab7862c-4c57-491e-8a45-d52a7e023983",
                    "scopes": [],
                    "redirectUrl": "https://logic-apis-eastus.consent.azure-apim.net/redirect",
                    "properties": {
                        "IsFirstParty": "True"
                    },
                    "customParameters": {
                        "tenantId": {},
                        "resourceUri": {
                            "value": "https://management.core.windows.net/"
                        }
                    }
                }
            },
            "token:clientId": {
                "type": "string",
                "uiDefinition": {
                    "displayName": "Client ID",
                    "description": "Client (or Application) ID of the Azure Active Directory application.",
                    "constraints": {
                        "required": "false",
                        "hidden": "true"
                    }
                }
            },
            "token:clientSecret": {
                "type": "securestring",
                "uiDefinition": {
                    "displayName": "Client Secret",
                    "description": "Client secret of the Azure Active Directory application.",
                    "constraints": {
                        "required": "false",
                        "hidden": "true"
                    }
                }
            },
            "token:TenantId": {
                "type": "string",
                "uiDefinition": {
                    "displayName": "Tenant",
                    "description": "The tenant of ID for the Azure Active Directory application.",
                    "constraints": {
                        "required": "false",
                        "hidden": "true"
                    }
                }
            },
            "token:resourceUri": {
                "type": "string",
                "uiDefinition": {
                    "displayName": "ResourceUri",
                    "description": "The resource you are requesting authorization to use.",
                    "constraints": {
                        "required": "false",
                        "hidden": "true"
                    }
                }
            },
            "token:grantType": {
                "type": "string",
                "allowedValues": [
                    {
                        "value": "code"
                    },
                    {
                        "value": "client_credentials"
                    }
                ],
                "uiDefinition": {
                    "displayName": "Grant Type",
                    "description": "Grant type",
                    "constraints": {
                        "required": "false",
                        "hidden": "true",
                        "allowedValues": [
                            {
                                "text": "Code",
                                "value": "code"
                            },
                            {
                                "text": "Client Credentials",
                                "value": "client_credentials"
                            }
                        ]
                    }
                }
            }
        },
        "metadata": {
            "source": "marketplace",
            "brandColor": "#56A0D7"
        },
        "runtimeUrls": [
            "https://logic-apis-eastus.azure-apim.net/apim/azureautomation"
        ],
        "generalInformation": {
            "iconUrl": "https://cpgeneralstore.blob.core.windows.net/icons/azureautomation.png",
            "displayName": "Azure Automation",
            "description": "Azure Automation provides tools to manage your cloud and on-premises infrastructure seamlessly.",
            "releaseTag": "Preview"
        },
        "capabilities": [
            "actions"
        ]
    },
    "id": "/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/providers/Microsoft.Web/locations/eastus/managedApis/azureautomation",
    "name": "azureautomation",
    "type": "Microsoft.Web/locations/managedApis",
    "location": "eastus"
}
```
