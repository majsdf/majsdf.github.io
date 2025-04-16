---
layout: default
---
# EventSearch

~~~powershell
#XPathフィルター
$filter=
"*[System[(EventID=102)]]
and 
*[EventData[Data[@Name='TaskName']='\特定のタスク']]"

#イベントをXMLで取得
$Event=Get-WinEvent -LogName "Microsoft-Windows-TaskScheduler/Operational" -FilterXPath $filter
$xml=[xml]$Event[0].ToXml()

#出力
$xml.Event.EventData.Data
~~~
