# Chocolatey

`Get-ExecutionPolicy`.
If it returns `Restricted`, then run
`Set-ExecutionPolicy AllSigned` or `Set-ExecutionPolicy Bypass -Scope Process`

``` Powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
