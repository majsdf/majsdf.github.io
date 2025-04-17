---
layout: default
---
# EventSearch

## イベントビューア
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
$xml.Event.EventData.Data[0].'#text'
$xml.Event.EventData.Data[1].'#text'
$xml.Event.EventData.Data[2].'#text'
~~~

## 資格情報
~~~powershell
$pass = "password" | ConvertTo-SecureString -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential "Administrator",$pass

$cred
~~~

## ドメインパスワード変更
~~~powershell
Set-ADAccountPassword -Identity $user -Reset -NewPassword $pass -PassThru -Server 10.1.1.1 -Credential $cred
~~~





