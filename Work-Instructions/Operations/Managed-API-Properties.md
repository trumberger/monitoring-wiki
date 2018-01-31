## Query
```
GET
https://management.azure.com/subscriptions/{subscriptionID}providers/Microsoft.Web/locations/{location}/managedApis/{name}?api-version=2016-06-01
```

## Application Insights
```
{
    "properties": {
        "name": "applicationinsights",
        "connectionParameters": {
            "username": {
                "type": "string",
                "uiDefinition": {
                    "displayName": "Application Id",
                    "description": "The unique, unchangeable identifier for this application.",
                    "tooltip": "Provide the API Id",
                    "constraints": {
                        "required": "true"
                    }
                }
            },
            "password": {
                "type": "securestring",
                "uiDefinition": {
                    "displayName": "API Key",
                    "description": "The API key to connect to Application Insights through the API.",
                    "tooltip": "Provide the API Key",
                    "constraints": {
                        "required": "true"
                    }
                }
            }
        },
        "metadata": {
            "source": "marketplace",
            "brandColor": "#68217A"
        },
        "runtimeUrls": [
            "https://logic-apis-eastus.azure-apim.net/apim/applicationinsights"
        ],
        "generalInformation": {
            "iconUrl": "https://az818438.vo.msecnd.net/icons/applicationinsights.png",
            "displayName": "Azure Application Insights",
            "description": "Azure Application Insights is an extensible analytics service that helps you understand the performance and usage of your live web application. Connect to your Application Insights resource to run and visualize various Analytics queries.",
            "releaseTag": "Preview"
        },
        "capabilities": [
            "actions"
        ]
    },
    "id": "/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/providers/Microsoft.Web/locations/eastus/managedApis/applicationinsights",
    "name": "applicationinsights",
    "type": "Microsoft.Web/locations/managedApis",
    "location": "eastus"
}
```

## Kusto

```
{
    "properties": {
        "name": "kusto",
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
                        "resourceUri": {
                            "value": "https://kusto.kustomfa.windows.net"
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
                    "description": "The tenant ID for the Azure Active Directory application.",
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
                    "description": "The resource you are requesting authorization to use, for instance https://kusto.kustomfa.windows.net.",
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
            "brandColor": "#2F2C69"
        },
        "runtimeUrls": [
            "https://logic-apis-eastus.azure-apim.net/apim/kusto"
        ],
        "generalInformation": {
            "iconUrl": "https://az818438.vo.msecnd.net/icons/kusto.png",
            "displayName": "Azure Kusto",
            "description": "Kusto is a log analytics cloud platform optimized for ad-hoc big data queries. Read more about it here: http://aka.ms/kdocs",
            "releaseTag": "Preview"
        },
        "capabilities": [
            "actions"
        ]
    },
    "id": "/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/providers/Microsoft.Web/locations/eastus/managedApis/kusto",
    "name": "kusto",
    "type": "Microsoft.Web/locations/managedApis",
    "location": "eastus"
}
```

## Log Analytics (Data Collector)

{
    "properties": {
        "name": "azureloganalyticsdatacollector",
        "connectionParameters": {
            "username": {
                "type": "string",
                "uiDefinition": {
                    "displayName": "Workspace ID",
                    "description": "The unique identifier of the Azure Log Analytics workspace.",
                    "tooltip": "Provide ID of the Azure Log Analytics workspace.",
                    "constraints": {
                        "required": "true"
                    }
                }
            },
            "password": {
                "type": "securestring",
                "uiDefinition": {
                    "displayName": "Workspace Key",
                    "description": "The primary or secondary key of the Azure Log Analytics workspace.",
                    "tooltip": "Provide primary or secondary key of the Azure Log Analytics workspace.",
                    "constraints": {
                        "required": "true"
                    }
                }
            }
        },
        "metadata": {
            "source": "marketplace",
            "brandColor": "#0072C6"
        },
        "runtimeUrls": [
            "https://logic-apis-eastus.azure-apim.net/apim/azureloganalyticsdatacollector"
        ],
        "generalInformation": {
            "iconUrl": "https://cpgeneralstore.blob.core.windows.net/icons/azureloganalyticsdatacollector.png",
            "displayName": "Azure Log Analytics Data Collector",
            "description": "Azure Log Analytics Data Collector will send data to any Azure Log Analytics workspace.",
            "releaseTag": "Preview"
        },
        "capabilities": [
            "actions"
        ]
    },
    "id": "/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/providers/Microsoft.Web/locations/eastus/managedApis/azureloganalyticsdatacollector",
    "name": "azureloganalyticsdatacollector",
    "type": "Microsoft.Web/locations/managedApis",
    "location": "eastus"
}

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
