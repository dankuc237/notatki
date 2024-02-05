```bash
$ nmap -sn <IP_range> # ping scan, network scan for hosts using ICMP
$ nmap -sn <IP_range> # ARP scan, network scan for hosts using ARP
$ nmap -sn <IP_range> [--send-ip] # ping scan, network scan for hosts using ICMP as privileged user
$ nmap -sn -PR <IP> # ARP network scan, IP=172.16.8.*
```

^91a985
