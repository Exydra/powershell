# Powershell

### ISE = Integrated Scripting Environment

### To check PS version number:
```
$PSVersionTable
```
### all .exe files in Sytstem32 folder and submaps:
```
Get-ChildItem -path C:\Wibndows\System32 -Filter *.exe
```
### Update Help content
```
Update-Help
```
### Info about command:
```
Get-Help Update-Help -Full
```
### Help with command structure(GUI):
```
Show-Command Get-ChildItem
```
# Powershell providers
File system = provider

Registery = privider

Function = provider

```
Get-PSProvider
```
### Returns all entries in register: HKEY Current USer
```
Set-Location HKCU:
Get-ChildItem
```
## Make directory, make Array of 50 lines, make for each object a new file with index token
```
New-Item -ItemType directory -Path D:\POWERSHELL\2.5
1..50 | ForEach-Object {New-Item -ItemType File -Path D:\POWERSHELL\2.5 -Name "File_$_.txt"}
```
### Copy Files
```
Copy-Item "D:\POWERSHELL\2.5" -Destination "D:\POWERSHELL\2.6\data_backup" -Recurse
```
### Stop print spooler
```
Get-Service -Name Spooler | Stop-Service
```
## Situations where you want to know what happens first:
```
-WhatIf
```
## Situations where you want to confirm actions:
```
-Confirm
```
# Exporting
## Output to CSV-File:
```
Get-ChildItem -Path 'C:\Program Files' -Recurse | Export-Csv C:\logboek.csv
```
opening it with notepad:
```
notepad C:\logboek.csv
```
## Output to XML-File
```
Get-ChildItem -Path 'C:\Program Files' -Recurse | Export-Clixml C:\logboek.csv
```
## Output to txt
```
Get-ChildItem -Path C:\data1\*.* | Out-File -FilePath C:\logboek.txt
```
## Output to GridView
```
Get-ChildItem C:\data1\*.* | Out-GridView
```
## All commands with out in it:
```
Get-Command -Verb out
```
## Ouput to HTML:
```
Get-ChildItem C:\data1\*.* | ConvertTo-Html | Out-File C:\archief.html
```
## List all processes, save it to txt, kill Notepad and Paint
```
Get-Process | Out-File processes.txt
Stop-Process -Name "Notepad" -Force
Stop-Process -Name "Paint" -Force
```
## Import files:
```
Import-Clixml -Path C:\logboek.xml
```
Read Files
```
Get-Content -Path C:\logboek.txt
```
# execute scripts
```
cmd: powershell.exe -noexit C:\scripts.ps1
powershell: 'move to path and ./script.ps1
```
## Get Execution Policy
```
Get-ExecutionPolicy
```
### 4 policies:
**Restricted:** je kunt geen gebruikmaken van scripts; alleen commando's rechtstreeks in PS worden geaccepteerd. Standaard voor Windows Server 2012R2

**AllSigned:** alleen scripts die ondertekend zinn door een 'trusted publisher' kunnen uitgevoerd worden.

**RemoteSigned:** gedownloade scripts moeten worden ondertekend zijn door een trusted publisher voordat ze worden uitgevoerd. Zelf gemaakte scripts worden wel uitgevoerd. Dat is de standaard vanaf Windows Server 2012R2 en dus ook voor windows Server 2016.

**Unrestricted:** alle scripts worden uitgevoerd, zonder restricties.

## Set new execution policy:
```
Set-ExecutionPolicy Unrestricted
```





# Variables
```
$a = 5
$b = 2
$som = $a + $b
$keer = $a * $b
'De som van ' + $a + ' en ' + $b + ' is gelijk aan ' + $som
```
## use backtick (`` ` ``) to comment out variable names
## List of all variables
```
Get-ChildItem Variable:
```
## Delete variable
```
Remove-Item Variable:c
```
## Delete all variables
```
Get-Variable | Remove-Variable
```
## powershell data types
```
Int
Long
String
Byte
Bool
Decimal
```
# Control strutures
## if, elseif and else
```
Clear-Host
[int]$number = Read-Host "Vul een getal tussen 1 en 10 in"
if ($number -gt 10) {
    Write-Host "Het getal is groter dan 10"}
elseif ($number -lt 10) {
    Write-Host "Het getal is kleiner dan 10"}
else {
    Write-Host "Het getal is precies 10"}
```
## ForEach, Array
```
Clear-Host
[array]$number = @(1,2,3,4,5,6,7,8,9,10)
Foreach ($a in $number)
{
    Write-Host $a
}
```
## Switch
```
Clear-Host
$number = Read-Host "Vul een getal in tussen 0 en 4"
Switch ($number){
    1 {Write-Host "Je hebt het getal 1 gekozen";break}
    2 {Write-Host "Je hebt het getal 2 gekozen"}
    3 {Write-Host "Je hebt het getal 3 gekozen"}
    Default {Write-Host "Je hebt niet het getal 1,2 of 3 gekozen"} 
}
```
## Do, while, until
```
Clear-Host
[int] $a = 0
Do {
    Write-Host "De waarde van `$a is $a"
    $a++

} while ($a -lt 10)
```
## For
```
Clear-Host
For ([int] $a = 0; $a -lt 100; $a++){
    Write-Host "De waarde van `$a is $a"
}
```
# 4.2:
```
Clear-Host

[int] $leeftijd = Read-Host "Wat is je leeftijd?"

if ($leeftijd -lt 16){
    Write-Host "De gebruiker is jonger dan 16 jaar."
} elseif ($leeftijd -lt 25){
    Write-Host "De gebruiker is jonger dan 25 jaar."
} elseif ($leeftijd -lt 40){
    Write-Host "De gebruiker is jonger dan 40 jaar."
} else {
    Write-Host "De gebruiker is ouder dan 40 jaar."
}
```
# 4.3:
```
Clear-Host

[int] $leeftijd = Read-Host "Wat is je leeftijd?"

if ($leeftijd -lt 16){
    Write-Host "De gebruiker is jonger dan 16 jaar."
} elseif ($leeftijd -lt 25){
    Write-Host "De gebruiker is jonger dan 25 jaar."
} elseif ($leeftijd -lt 40){
    Write-Host "De gebruiker is jonger dan 40 jaar."
} else {
    Write-Host "De gebruiker is ouder dan 40 jaar."
}
```
# 4.4
```
Clear-Host
$set1 = (Get-Date).AddDays(-10)
$set2 = (Get-Date).AddDays(-20)
$set3 = (Get-Date).AddDays(-30)
$set4 = (Get-Date).AddDays(-40)

Get-Item C:\data1\file_?.txt | foreach-object {$_.Creationtime = $set1}
Get-Item C:\data1\file_1?.txt | foreach-object {$_.Creationtime = $set2}
Get-Item C:\data1\file_2?.txt | foreach-object {$_.Creationtime = $set3}
Get-Item C:\data1\file_3?.txt | foreach-object {$_.Creationtime = $set4}

$days = (Get-Date).AddDays(-20)
Get-ChildItem -Path C:\data1 -Recurse -Force | where-object {!$_.PSIscontainer -and $_.CreationTime -lt $days} | Remove-Item

$tdc='C:\data1'
$a = Get-ChildItem $tdc -recurse | Where-Object {$_.PSIsContainer -eq $True}
$a | Where-Object {$_.GetFiles().Count -eq 0} | Remove-Item
```
# 4.5
```
clear-host
$Username = Get-Content Env:USERNAME 
$Computername = get-content env:COMPUTERNAME
$Datum = Get-Date -Format "dd-MM-yyyy HH:mm"
$IPaddress = Get-NetIPAddress -IPAddress 10.0.*.* | Select-Object -ExpandProperty IPAddress 
$text = "Login: [" + $Username + " | " + $Computername + " | " + $Datum + " | " + $IPaddress + "]"

$text | Out-file -append -FilePath C:\logon.txt
```
# 4.6
### Comments in powershell: `#`
```
<#
.SYNOPSIS       
		logonscript wordt uitgevoerd bij het aanmelden

.DISCRIPTION    Dit script maakt een log bestand aan met
                - Gebruikersnaam
                - Computernaam
                - Datum en tijd
                - IPAdres
                elke keer als een gebruiker aanmeld

.PARAMETER <[INT]leeftijd >

.EXAMPLE        ./script

.NOTES          Leer werken met PowerShell - Roland Sellis

                Naam: 
                Klas: 
                Nummer:

.LINK           kaka@gmail.com
#>
clear-host
$Username = Get-Content Env:USERNAME 
$Computername = get-content env:COMPUTERNAME
$Datum = Get-Date -Format "dd-MM-yyyy HH:mm"
$IPaddress = Get-NetIPAddress -IPAddress 10.0.*.* | Select-Object -ExpandProperty IPAddress 
$text = "Login: [" + $Username + " | " + $Computername + " | " + $Datum + " | " + $IPaddress + "]"

$text | Out-file -append -FilePath C:\logon.txt
```
# 7.1
```
Set-ADUser -Identity ll-22222 -Company Mediatech -Department IT -EmailAddress ll-22222@broeders.be
Get-ADuser -Identity ll-22222 -Properties *|format-table emailaddress,company,department
```
# 7.2
```
New-ADOrganizationalUnit -Name Sint-Niklaas
New-ADGroup -Name IT -Path "ou=Sint-Niklaas, DC=mediatech, DC=lan"
Add-ADGroupMember -Identity IT-Members bep
```
# 7.3
```
New-ADGroup -GroupScope Global -Name Sales -Path "ou=Sint-Niklaas, dc=MediaTech, dc=lan"
Add-ADGroupMember -Identity Sales -Members BEP
Set-ADUser -Identity BEP -Department Sales
Add-ADGroupMember -Identity IT -Members BEP
```
# 7.4
```
$VoornaamNaam = "Jef DeBauwer"
$Naam = "DeBauwer"
$Wachtwoord = Read-Host "Wachtwoord?????????"

New-ADUser -name $VoornaamNaam -AccountPassword (ConvertTo-SecureString -AsPlainText $Wachtwoord -Force) `
-DisplayName $VoornaamNaam `
-SamAccountName $Naam `
-Enabled $true
```
