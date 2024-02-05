```bash
$ namp <IP> -p 22 
$ namp <IP> -p 22  --script ssh-auth-methods [--script-args="ssh.user=admin"]
$ namp <IP> -p 22  --script ssh2-enum-algos
$ namp <IP> -p 22  --script ssh-hostkey [--script-args ssh_hostkey=full]
$ namp <IP> -p 22  --script ssh-run [--script-args="ssh-run.cmd=ls -la /, ssh-run.username=username, ssh-run.password=passwd"]
```