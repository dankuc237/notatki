```bash
$ nmap -p445 --script smb-protocols <IP> # identify all the supported SMB versions
$ nmap -p445 --script smb-security-mode <IP> # identify the smb protocol security level
$ nmap -p445 --script smb-enum-users <IP> # enumerate SMB users >> hydra
$ nmap -sU -p U:137,T:139 -sS --script smb-enum-users  <IP> # enumerate SMB users >> hydra
$ nmap <IP> -p445 --script smb-enum-shares [--script-args smbusername=<username>,smbpassword=<passwd>]
$ nmap <IP> -p445 --script smb-enum-domains [--script-args smbusername=<username>,smbpassword=<passwd>]
$ nmap <IP> -p445 --script smb-enum-groups [--script-args smbusername=<username>,smbpassword=<passwd>]
$ nmap <IP> -p445 --script smb-enum-shares,smb-ls [--script-args smbusername=<username>,smbpassword=<passwd>]
```
