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
###Analysis