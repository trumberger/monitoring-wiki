# Overview
If you receive notification that the system has failed to create an ICM Ticket (or, more likely, several notifications) then here's how you can investigate.

For the investigation, you should use Kusto queries against the Business Logic App Insights instance for the environment that failed.
For PROD (AIS-PROD-NativeMonitoring), this is at [this link](https://analytics.applicationinsights.io/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourcegroups/PROD-BusinessLogic/components/AIS-PROD-NativeMonitoring#/discover/home?apptype=web&resourceId=%252Fsubscriptions%252F16b26395-68e3-45e2-81c1-54729c26aba8%252Fresourcegroups%252FPROD-BusinessLogic%252Fproviders%252Fmicrosoft.insights%252Fcomponents%252FAIS-PROD-NativeMonitoring).

# Queries
**Note, all the examples below include a time range of the last 24h - "> ago(24h)". Remember to adjust this for your investigation if needed.**


## Step 1: Discover why the calls to ICM failed
### Query
requests
| union exceptions
|  where timestamp > ago(24h) and operation_Name == 'ICM-CreateTicket' and coalesce(success, 'False') == 'False'
| project timestamp, operation_Name, coalesce(innermostMessage, '(failed request)') 
| order by timestamp

### Example output
<TABLE class=MsoNormalTable border=0 cellspacing=0 cellpadding=0 width=699 style="width:524.2pt;margin-left:.05pt;border-collapse:collapse">
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border:solid #8EA9DB 1.0pt;border-right:none;background:#4472C4;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><B><SPAN style="color:white">timestamp</SPAN></B></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border-top:solid #8EA9DB 1.0pt;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:none;background:#4472C4;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><B><SPAN style="color:white">operation_Name</SPAN></B></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border:solid #8EA9DB 1.0pt;border-left:none;background:#4472C4;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><B><SPAN style="color:white">Column1</SPAN></B></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:34.106Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">The
  remote server returned an error: (503) Server Unavailable.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:33.821Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">(failed
  request)</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:33.665Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">The
  remote server returned an error: (503) Server Unavailable.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:33.446Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">(failed
  request)</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:33.259Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">The
  remote server returned an error: (503) Server Unavailable.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:32.978Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">(failed
  request)</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:32.837Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">The
  remote server returned an error: (503) Server Unavailable.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:32.634Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">(failed
  request)</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:32.504Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">The
  remote server returned an error: (503) Server Unavailable.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=184 nowrap valign=bottom style="width:137.95pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">2018-05-17T04:49:32.301Z</SPAN></P>
  </TD>
  <TD width=118 nowrap valign=bottom style="width:88.55pt;border:none;border-bottom:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">ICM-CreateTicket</SPAN></P>
  </TD>
  <TD width=397 nowrap valign=bottom style="width:297.7pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">(failed
  request)</SPAN></P>
  </TD>
 </TR>
</TABLE>

### Analysis
In the output above, you can see that each failed request corresponds with an exception of a 503 response from the server. This suggests an IcM Outage.

## Step 2: Discover the Impacted Customers
###Query
exceptions 
| where timestamp > ago(24h)
| join traces on operation_Id
| where message1 contains 'certificate'
| project timestamp,innermostMessage, message1
| summarize count() by message1

###Example Output
<TABLE class=MsoNormalTable border=0 cellspacing=0 cellpadding=0 width=276 style="width:207.0pt;margin-left:.05pt;border-collapse:collapse">

 <TR style="height:14.25pt">
  <TD width=212 nowrap valign=bottom style="width:159.0pt;border:solid #8EA9DB 1.0pt;border-right:none;background:#4472C4;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><B><SPAN style="color:white">message1</SPAN></B></P>
  </TD>
  <TD width=64 nowrap valign=bottom style="width:48.0pt;border:solid #8EA9DB 1.0pt;border-left:none;background:#4472C4;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><B><SPAN style="color:white">count_</SPAN></B></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=212 nowrap valign=bottom style="width:159.0pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">Certificate
  set: mc-track-connector</SPAN></P>
  </TD>
  <TD width=64 nowrap valign=bottom style="width:48.0pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;background:#D9E1F2;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal align=right style="text-align:right"><SPAN style="color:black">62</SPAN></P>
  </TD>
 </TR>
 <TR style="height:14.25pt">
  <TD width=212 nowrap valign=bottom style="width:159.0pt;border-top:none;border-left:solid #8EA9DB 1.0pt;border-bottom:solid #8EA9DB 1.0pt;border-right:
  none;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal><SPAN style="color:black">Certificate
  set: kpmg-ob-connector</SPAN></P>
  </TD>
  <TD width=64 nowrap valign=bottom style="width:48.0pt;border-top:none;border-left:none;border-bottom:solid #8EA9DB 1.0pt;border-right:solid #8EA9DB 1.0pt;padding:0cm 5.4pt 0cm 5.4pt;height:14.25pt">
  <P class=MsoNormal align=right style="text-align:right"><SPAN style="color:black">70</SPAN></P>
  </TD>
 </TR>
</TABLE>

###Analysis
There were 62 failed alerts for MC-TRACK and 70 for KPMG-OB

## Step 3: Discover the Specific Alerts That Failed
###Query
exceptions
| where timestamp > ago(24h)
| join
    traces
on operation_Id
| where message1 contains 'Queue Message'
| join
    traces
on operation_Id
| where message2 contains 'certificate'
| project timestamp, message1, message2
| summarize count() by message2, message1
| order by message2, count_, message1

###Example Output
<TABLE>
<COL width=96 style="width:72pt"/>

 <COL width=515 style="width:386pt"/>
 <COL width=109 style="width:81pt"/>
 <TR style="height:14.25pt">
  <TD height=19 width=96 style="height:14.25pt;width:72pt;font-size:11.0pt;color:white;font-weight:700;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB;background:#4472C4">message2</TD>
  <TD width=515 style="width:386pt;font-size:11.0pt;color:white;font-weight:
  700;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#4472C4">message1</TD>
  <TD width=109 style="width:81pt;font-size:11.0pt;color:white;font-weight:
  700;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#4472C4">count_</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB;background:#D9E1F2">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">Queue Message:
  {&quot;Name&quot;:&quot;Unusual Peak in HTTP 4xx
  messages&quot;,&quot;Description&quot;:&quot;Unusual peak in 4xx errors
  coming from the application
  endpoints&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-16T22:13:15&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot; **REDACTED** \&quot;,11]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none">Queue Message: {&quot;Name&quot;:&quot;Unusual Peak in HTTP
  4xx messages&quot;,&quot;Description&quot;:&quot;Unusual peak in 4xx errors
  coming from the application
  endpoints&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T01:56:54&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**\&quot;,12],[\&quot;\&quot;,12]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB;background:#D9E1F2">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">Queue Message:
  {&quot;Name&quot;:&quot;Unusual Peak in HTTP 4xx
  messages&quot;,&quot;Description&quot;:&quot;Unusual peak in 4xx errors
  coming from the application
  endpoints&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T00:14:44&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**;,11]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none">Queue Message: {&quot;Name&quot;:&quot;Unusual Peak in HTTP
  4xx messages&quot;,&quot;Description&quot;:&quot;Unusual peak in 4xx errors
  coming from the application
  endpoints&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-16T22:26:32&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**\&quot;,52]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none">5</TD>
 </TR>
  
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB;background:#D9E1F2">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">Queue Message:
  {&quot;Name&quot;:&quot;Too many failed VM logon
  attempts&quot;,&quot;Description&quot;:&quot;Checks the number of failed
  authentications on one or multiple
  VMs&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T01:57:49&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;\\\\**REDACTED**\&quot;,12]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none">Queue Message: {&quot;Name&quot;:&quot;Computers that
  failed baseline security rules&quot;,&quot;Description&quot;:&quot;VMs
  detected that are not in compliance with security baseline (in
  SC)&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T04:49:28&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**\&quot;],[\&quot;mcperfvm\&quot;]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB;background:#D9E1F2">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">Queue Message:
  {&quot;Name&quot;:&quot;Computers that failed baseline security
  rules&quot;,&quot;Description&quot;:&quot;VMs detected that are not in
  compliance with security baseline (in
  SC)&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T01:58:09&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**\&quot;],[\&quot;**REDACTED**\&quot;],[\&quot;mcperfvm\&quot;]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none">Queue Message: {&quot;Name&quot;:&quot;Unusual Peak in HTTP
  4xx messages&quot;,&quot;Description&quot;:&quot;Unusual peak in 4xx errors
  coming from the application
  endpoints&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-16T20:08:16&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none">1</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB;background:#D9E1F2">mc-track</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">Queue Message:
  {&quot;Name&quot;:&quot;Computers that failed baseline security
  rules&quot;,&quot;Description&quot;:&quot;VMs detected that are not in
  compliance with security baseline (in
  SC)&quot;,&quot;Customer&quot;:&quot;MasterCard&quot;,&quot;ServiceID&quot;:&quot;MC-TRACK&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-16T21:09:42&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**\&quot;],[\&quot;**REDACTED**\&quot;]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">1</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB">kpmg-ob</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none">Queue Message: {&quot;Name&quot;:&quot;Computers that
  failed baseline security rules&quot;,&quot;Description&quot;:&quot;VMs
  detected that are not in compliance with security baseline (in
  SC)&quot;,&quot;Customer&quot;:&quot;KPMG&quot;,&quot;ServiceID&quot;:&quot;KPMG-OB&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T04:46:01&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**\&quot;]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB;background:#D9E1F2">kpmg-ob</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">Queue Message:
  {&quot;Name&quot;:&quot;Computers that failed baseline security
  rules&quot;,&quot;Description&quot;:&quot;VMs detected that are not in
  compliance with security baseline (in
  SC)&quot;,&quot;Customer&quot;:&quot;KPMG&quot;,&quot;ServiceID&quot;:&quot;KPMG-OB&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T03:03:54&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot**REDACTED**\&quot;]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none;background:#D9E1F2">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 style="height:14.25pt;font-size:11.0pt;color:black;font-weight:
  400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  none;border-bottom:.5pt solid #8EA9DB;border-left:.5pt solid #8EA9DB">kpmg-ob</TD>
  <TD style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:none;border-bottom:.5pt solid #8EA9DB;border-left:none">Queue Message: {&quot;Name&quot;:&quot;Computers that
  failed baseline security rules&quot;,&quot;Description&quot;:&quot;VMs
  detected that are not in compliance with security baseline (in
  SC)&quot;,&quot;Customer&quot;:&quot;KPMG&quot;,&quot;ServiceID&quot;:&quot;KPMG-OB&quot;,&quot;Severity&quot;:2,&quot;Environment&quot;:&quot;**REDACTED**&quot;,&quot;Category&quot;:&quot;Security&quot;,&quot;Source&quot;:&quot;LogAnalytics&quot;,&quot;TimeCreated&quot;:&quot;2018-05-17T02:25:31&quot;,&quot;ScenariosImpacted&quot;:&quot;&quot;,&quot;EntitiesImpacted&quot;:&quot;&quot;,&quot;ResourcesImpacted&quot;:&quot;[[\&quot;**REDACTED**\&quot;],[\&quot;**REDACTED**\&quot;]]&quot;,&quot;Instance&quot;:&quot;Single
  Instance&quot;,&quot;TicketID&quot;:null}</TD>
  <TD align=right style="font-size:11.0pt;color:black;font-weight:400;text-decoration:none;font-family:Calibri, sans-serif;border-top:.5pt solid #8EA9DB;border-right:
  .5pt solid #8EA9DB;border-bottom:.5pt solid #8EA9DB;border-left:none">5</TD>
 </TR>
</TABLE>

###Analysis
By doing some simple parsing of these results in Excel you can distill it down to the following, showing which alerts were lost for which customers and their count. Where the same alert name appears on multiple rows, that means that different resources were impacted for each of those different lines.

Note also that where count > 1, the subsequent alerts would likely have been suppressed. So for the data below we can summarise that both KPMG and MC-TRACK have lost 14 alerts (as there are 14 rows for each of the services in the table).

<TABLE>
<COL width=96 style="width:72pt"/>

 <COL width=368 style="width:276pt"/>
 <COL width=109 style="width:81pt"/>
 <TR style="height:14.25pt">
  <TD height=19 class=xl65 width=96 style="height:14.25pt;width:72pt">Service</TD>
  <TD class=xl65 width=368 style="width:276pt">Alert</TD>
  <TD class=xl65 width=109 style="width:81pt">Count</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Unusual Peak in HTTP 4xx message</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl70 style="border-top:none">Unusual Peak in HTTP 4xx message</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Unusual Peak in HTTP 4xx message</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl70 style="border-top:none">Unusual Peak in HTTP 4xx message</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Unusual Peak in HTTP 4xx message</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl70 style="border-top:none">Unusual Peak in HTTP 4xx message</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Unauthorized access to VM�</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Unauthorized access to Keyvault</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl70 style="border-top:none">Unauthorized access to Keyvault</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Too many failed VM logon attempt</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl70 style="border-top:none">Unusual Peak in HTTP 4xx message</TD>
  <TD class=xl71 align=right style="border-top:none">1</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">mc-track</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">1</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl67 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl69 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl70 style="border-top:none">Computers that failed baseline
  security rule</TD>
  <TD class=xl71 align=right style="border-top:none">5</TD>
 </TR>
 <TR style="height:14.25pt">
  <TD height=19 class=xl66 style="height:14.25pt;border-top:none">kpmg-ob</TD>
  <TD class=xl67 style="border-top:none">Azure Resource delete</TD>
  <TD class=xl68 align=right style="border-top:none">5</TD>
 </TR>