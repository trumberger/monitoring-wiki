# References

**Telemetry correlation docs**
[https://docs.microsoft.com/azure/application-insights/application-insights-correlation]()

**Activity User Guide**
[https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticsSource/src/AcitivityUserGuide.md]()

**Custom operations tracking**
[https://docs.microsoft.com/azure/application-Insights/application-insigths-custom-operations-tracking]()

**Kusto information**
[https://microsoft.sharepoint.com/teams/kusto/SitePages/Home.aspx]()
[http://resnet/resnet/fullvideo.aspx?id=38651]() 

**Kusto Query Language**
[Official Site](https://docs.loganalytics.io/index)

# Custom Events

##Query Custom Events
In Log Analytics custom properties can be extracted using regular expression:

`extract("\"{Custom Event Property}\": \"(.*)\"", 1, CustomEventDimensions)`

**ESS Alert Example**

Following query retrieves custom properties from alert event:

```
ApplicationInsights
| where TelemetryType == "CustomEvent" and CustomEventName == "AlertReceived"
| extend Customer = extract("\"customer\": \"(.*)\"", 1, CustomEventDimensions)   
| extend ServiceID = extract("\"serviceID\": \"(.*)\"", 1, CustomEventDimensions)   
| extend AlertName = extract("\"alertName\": \"(.*)\"", 1, CustomEventDimensions)
| extend Severity = extract("\"severity\": \"(.*)\"", 1, CustomEventDimensions)
| project Customer, ServiceID, AlertName, Severity
```
 
