For Log Analytics the schema should be:

    {
      "alertName": "Unusual Peak in HTTP 4xx messages",
      "description": "Unusual peak in 4xx errors coming from the application endpoints",
      "severity": 2,
      "query": "AzureMetrics| where ResourceProvider == \"MICROSOFT.WEB\" | where MetricName == \"Http4xx\"| where Total != 0| summarize Errors = count() by Resource| where Errors > 10 ",
      "searchCategory": "Security",
      "source": "LogAnalytics"
    }

For Application Insights the schema should be:

    {
      "alertName": "Get requests in the last 7 days",
      "description": "Get request in the last 7 days",
      "severity": 2,
      "query": "requests | where timestamp > ago(7d) | summarize count() by client_CountryOrRegion",
      "searchCategory": "Availability",
      "source": "ApplicationInsights",
      "sourceInstance": "f5a290bf-bab4-46b6-b38a-26089ad7a8f3"
    }

Note: The parameter sourceInstance is required when creating alert rules for Application Insights.