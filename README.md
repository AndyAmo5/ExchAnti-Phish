# ExchAnti-Phish

Using data from @SwiftOnSecurity Swiftfilter this is put into a format I can use to import the rules into Office 365 transport rules. 

Usage: 
Backup existing rules first....
```
$file = Export-TransportRuleCollection
Set-Content -Path "Rules1.xml" -Value $file.FileData -Encoding Byte
```

```
Set-ExecutionPolicy RemoteSigned
$credential = Get-Credential    
$exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection
Import-PSSession $exchangeSession
[Byte[]]$Data = Get-Content -Path "Full-Path-To-Rules.xml" -Encoding Byte -ReadCount 0
Import-TransportRuleCollection -FileData $Data
```