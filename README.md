
# Get-SPFarmLogs

**This script permits to collect multiple kind of logs in a SharePoint farm or for a group of servers. You have an extended farm and you need to collect logs in each one of your 5, 6 or 10 servers. It’s a waste of time to logon one by one to do that!! With this script you can collect Farm’s Logs to a centralized folder.**
** **
**donwload the [last release](https://github.com/MigueGo/Get-SPFarmLogs/releases/latest) from here.**

## Syntax

```powershell 
  .\get-spfarmlogs.ps1  `
  -EventsDir "C:\folder\logs" `
  -ULSstarttime "01/jan/2019 08:30" `
  -ULSendtime "01/jan/2019 09:32" `
  -IISdate 18010 `
  -NoEvents:$false `
  -Servers "SP,SQL,DC"

  This command permits to gather all the logs from all the specfied servers : EventViewer, IIS and ULS log  in the folder "C:\folder\logs".
 ```
 ```powershell 
   .\get-spfarmlogs.ps1 -user contoso\administrator `
   -EventsDir "C:\folder\logs" `
   -servers "SP,SP2" `
   -IISdate 17010 `
   -NoEvents:$false; 
    
    this command permits to gather the EventViewer and IIS logs in the folder "C:\folder\logs" for the servers SP and SP2, there is no ULS logs collected.
 
```
```powershell 
    $starttime = (Get-Date "03/may/2021 09:00"); #specify the estimated time that the issue started 
    $endtime = (Get-Date "03/may/2021 09:15"); #specify the estimated time that the issue ended
    $iisdate = $EndTime.ToString("yyMMdd");
    $ftag = $EndTime.ToString("yyMMdd-HHmm");
    
  .\get-spfarmlogs.ps1  -EventsDir "c:\temp\logs\MSLogs_$foldertag" `
    -ULSstarttime $StartTime  `
    -ULSendtime $EndTime  `
    -IISdate $iisdate  `
    -NoEvents:$false 

  This command permits to gather all the logs from all servers of the farm : EventViewer, IIS and ULS log  in the folder "c:\temp\logs\MSLogs_$foldertag".
 ```

note: it's important to run your Powershell console in administrator mode.

## Detailed Description

**this is a script to be run in PowerShell UI (like PowerShell ISE) or a Powershell window. The loading of the SharePoint module is already included in the script.**

**donwload the [last release](https://github.com/MigueGo/Get-SPFarmLogs/releases/latest) from here.**



| Parameter     | Description      | default value    |
| ------------- | ---------------- | ----------------:|
| -user         | user with administrator rights on all the servers                                                        | N/A    |
| -NoEvents     | syntax: -NoEvents:$true or -NoEvents:$false indicate if Application or System event viewer are required  | $false |
| -EventsDir    | define the folder where the logs will be saved. If the folder doesn't exist it will be created   | N/A |
| -IISdate      | this is a multivalue switch, between "" you can add different time date. it also defines the wildcard value for the IIS logs to gather, i.e 17010 will collect all IIS logs between 170101 to 170109. The default format in IIS is YYMMDD |if not specified the IIS logs will not be collected     |
| -servers      | between quotation mark "" you specify the list of the servers that will be collected, the separator is the coma (,)| if not specified all the servers of the farm will be collected   |
| -ULSstarttime | start time for collection ULS logs in each server of the list. Time is local time on the server. ex: "23/jan/2019 14:15:30"  | N/A      |
| -ULSendtime   | end time for collection ULS logs in each server of the list. Time is local time on the server. ex: "23/jan/2019 14:30:00" | N/A      |





