Netcat: The powershell version.
/usr/share/windows-resources/powercat
```PowerShell
# Load The Function From Downloaded .ps1 File:
. .\powercat.ps1                                                          # Load The Function From URL:
IEX (New-Object System.Net.Webclient).DownloadString('https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1')
```