<!-- TOC -->

- [SKANOWANIE W POSZUKIWANIU OTWARTYCH PORTÓW](#skanowanie-w-poszukiwaniu-otwartych-portów)
  - [szybki skan TCP](#szybki-skan-tcp)
  - [pełny skan TCP](#pełny-skan-tcp)
  - [szybki skan UDP](#szybki-skan-udp)
- [ENUMERACJA ZNALEZIONYCH PORTÓW](#enumeracja-znalezionych-portów)
  - [FTP (20-pliki, 21-polecenia)](#ftp-20-pliki-21-polecenia)
    - [nmap skrypt](#nmap-skrypt)
  - [SSH 22](#ssh-22)
    - [nmap skrypt](#nmap-skrypt-1)
    - [bruteforce logins](#bruteforce-logins)
  - [SMTP (25)](#smtp-25)
    - [nmap skrypt](#nmap-skrypt-2)
    - [user enumeration](#user-enumeration)
    - [password bruteforce](#password-bruteforce)
  - [DNS (53)](#dns-53)
    - [nmap skrypty](#nmap-skrypty)
    - [DNS lookup](#dns-lookup)
    - [DNS zone trasfer](#dns-zone-trasfer)
    - [bruteforce subdomains of a DNS domain](#bruteforce-subdomains-of-a-dns-domain)
    - [automatically query data from the DNS server](#automatically-query-data-from-the-dns-server)
  - [HTTP (80)](#http-80)
    - [nmap skrypty](#nmap-skrypty-1)
    - [enumeracja subdomen bruteforce](#enumeracja-subdomen-bruteforce)
    - [enumeracje folderów bruteforce](#enumeracje-folderów-bruteforce)
    - [retreive web headers and find host information](#retreive-web-headers-and-find-host-information)
    - [web server full enumeration tool](#web-server-full-enumeration-tool)
    - [identyfikacja technologii użytych na stronie](#identyfikacja-technologii-użytych-na-stronie)
    - [Word Press](#word-press)
  - [POP3 (110)](#pop3-110)
    - [nmap skrypty](#nmap-skrypty-2)
  - [IMAP (143)](#imap-143)
    - [nmap skrypty](#nmap-skrypty-3)
  - [SMB (TCP 139,445)](#smb-tcp-139445)
    - [nmap skrypty](#nmap-skrypty-4)
  - [SNMP (161)](#snmp-161)
    - [nmap skrypty](#nmap-skrypty-5)
  - [RDP (3389)](#rdp-3389)
    - [nmap skrypty](#nmap-skrypty-6)
  - [VNC (TCP 5900 – 5906)](#vnc-tcp-5900--5906)
    - [nmap skrypty](#nmap-skrypty-7)
  - [Unidentified service](#unidentified-service)
    - [nmap skrypty](#nmap-skrypty-8)
- [BAZY DANYCH](#bazy-danych)
  - [MSSQL](#mssql)
    - [nmap skrypty](#nmap-skrypty-9)
  - [MySQL](#mysql)
    - [nmap skrypty](#nmap-skrypty-10)
  - [Oracle](#oracle)
    - [nmap skrypty](#nmap-skrypty-11)
  - [NFS](#nfs)
    - [nmap skrypty](#nmap-skrypty-12)

<!-- /TOC -->
# SKANOWANIE W POSZUKIWANIU OTWARTYCH PORTÓW
## szybki skan TCP
```bash
nmap -vv --reason -Pn -T4 -sV -sC --version-all -A --osscan-guess -oN "quick_tcp_nmap.txt" <ADDRES_IP>
```
## pełny skan TCP 
```bash
nmap -vv --reason -Pn -T4 -sV -sC --version-all -A --osscan-guess -p- -oN "full_tcp_nmap.txt" <ADDRES_IP>
```
## szybki skan UDP
```bash
nmap -vv --reason -Pn -T4 -sU -A --top-ports 100 -oN "top_100_udp_nmap.txt" <ADDRES_IP>
```

# ENUMERACJA ZNALEZIONYCH PORTÓW 
## FTP (20-pliki, 21-polecenia)
### nmap skrypt
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(ftp*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_ftp_nmap.txt" -oX "{basedir}/{port}_ftp_nmap.xml" {address}
```
## SSH 22
### nmap skrypt
```bash
nmap -vv --reason -Pn -T4 -sV -p 22 --script="banner,ssh2-enum-algos,ssh-hostkey,ssh-auth-methods" -oN "tcp_22_ssh_nmap.txt" <ADDRES_IP>
```
### bruteforce logins
```bash
hydra -L "/usr/share/seclists/Usernames/top-usernames-shortlist.txt" -P "/usr/share/seclists/Passwords/darkweb2017-top100.txt" -e nsr -s 22 -o "/home/kck/Downloads/trick/results/<ADDRES_IP>/scans/tcp22/tcp_22_ssh_hydra.txt" ssh://<ADDRES_IP>
medusa -U "/usr/share/seclists/Usernames/top-usernames-shortlist.txt" -P "/usr/share/seclists/Passwords/darkweb2017-top100.txt" -e ns -n 22 -O "/home/kck/Downloads/trick/results/<ADDRES_IP>/scans/tcp22/tcp_22_ssh_medusa.txt" -M ssh -h <ADDRES_IP>
```
## SMTP (25)
### nmap skrypt
```bash
nmap -vv --reason -Pn -T4 -sV -p 25 --script="banner,(smtp* or ssl*) and not (brute or broadcast or dos or external or fuzzer)" -oN "tcp_25_smtp_nmap.txt" <ADDRES_IP>
```
### user enumeration
using "RCPT TO"
```bash
hydra smtp-enum://<ADDRES_IP>:25/rcpt -L "/usr/share/seclists/Usernames/top-usernames-shortlist.txt" -o "/home/kck/Downloads/trick/results/<ADDRES_IP>/scans/tcp25/tcp_25_smtp_user-enum_hydra_rcpt.txt" -p <TARGET-DOMAIN>
```
### password bruteforce
```bash
hydra smtp-enum://<ADDRES_IP>:25/vrfy -L "/usr/share/seclists/Usernames/top-usernames-shortlist.txt" 2>&1
hydra smtp-enum://<ADDRES_IP>:25/expn -L "/usr/share/seclists/Usernames/top-usernames-shortlist.txt" 2>&1
```
## DNS (53)
### nmap skrypty
```bash
nmap -vv --reason -Pn -T4 -sV -p 53 --script="banner,(dns* or ssl*) and not (brute or broadcast or dos or external or fuzzer)" -oN "tcp_53_dns_nmap.txt" <ADDRES_IP>
```
### DNS lookup
```bash
dig -p 53 -x <ADDRES_IP> @<ADDRES_IP>
```
<details>
<summary>PARAMETERS</summary>
-p port na który wysłać zapytanie

-x addr
</details>

### DNS zone trasfer
```bash
dig AXFR -p 53 @<ADDRES_IP_DNS>
dig AXFR -p 53 @<ADDRES_IP_DNS> <ADDRES_IP>
```
### bruteforce subdomains of a DNS domain
```bash
dnsrecon -n <ADDRES_IP> -d <DOMAIN-NAME> -D /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t brt 2>&1 | tee /home/kck/Downloads/trick/results/<ADDRES_IP>/scans/tcp53/tcp_53_dnsrecon_subdomain_bruteforce.txt
```
### automatically query data from the DNS server
```bash
dnsrecon -n <ADDRES_IP> -d <DOMAIN-NAME> 2>&1 | tee /home/kck/Downloads/trick/results/<ADDRES_IP>/scans/tcp53/tcp_53_dnsrecon_default_manual.txt
```
## HTTP (80)
### nmap skrypty
```bash
nmap -vv --reason -Pn -T4 -sV -p 80 --script="banner,(http* or ssl*) and not (brute or broadcast or dos or external or http-slowloris* or fuzzer)" -oN "tcp_80_http_nmap.txt" <ADDRES_IP>
```
### enumeracja subdomen bruteforce
```bash
gobuster dns -d <ADDRES_IP> -r <ADDRES_IP> -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -o "tcp_53_<ADDRES_IP>_subdomains_subdomains-top1million-110000.txt"
ffuf -u http://<ADDRES_IP>:80/ -t 10 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.<ADDRES_IP>" -fs 5480 -noninteractive -s | tee "tcp_80_http_<ADDRES_IP>_vhosts_subdomains-top1million-110000.txt"
```
### enumeracje folderów bruteforce
```bash
feroxbuster -u http://<ADDRES_IP>:80/ -t 10 -w .../wordlists/dirbuster.txt -x "txt,html,php,asp,aspx,jsp" -v -k -n -q -e -o "tcp_80_http_feroxbuster_dirbuster.txt"
feroxbuster -u http://<ADDRES_IP>:80 -t 10 -w .../wordlists/dirbuster/directory-list-2.3-medium.txt -x "txt,html,php,asp,aspx,jsp" -v -k -n -e -o .../tcp_80_http_feroxbuster_dirbuster.txt
```
### retreive web headers and find host information
```bash
curl -sSikf http://<ADDRES_IP>:80/.well-known/security.txt
curl -sSikf http://<ADDRES_IP>:80/robots.txt
curl -sSik http://<ADDRES_IP>:80/
```
<details>
<summary>PARAMETERS</summary>

-s silent  
-S Show error even when -s is used   
-i Include protocol response headers in the output  
-k Allow insecure server connections    
-f Fail fast with no output at all on server errors.

</details>



### web server full enumeration tool
```bash
nikto -ask=no -h http://<ADDRES_IP>:80 2>&1 | tee "/home/kck/Downloads/trick/results/<ADDRES_IP>/scans/tcp80/tcp_80_http_nikto.txt"
```
### identyfikacja technologii użytych na stronie
```bash
whatweb --color=never --no-errors -a 3 -v http://<ADDRES_IP>:80 2>&1
```

### Word Press
```bash
wpscan --url http://<ADDRES_IP>:80/ --no-update -e vp,vt,tt,cb,dbe,u,m --plugins-detection aggressive --plugins-version-detection aggressive -f cli-no-color 2>&1 | tee "/home/kck/Downloads/trick/results/<ADDRES_IP>/scans/tcp80/tcp_80_http_wpscan.txt"
```

## POP3 (110)
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(pop3*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_pop3_nmap.txt" {address}
```
## IMAP (143) 
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(imap*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_imap_nmap.txt" -oX "{basedir}/{port}_imap_nmap.xml" {address}'
```
## SMB (TCP 139,445)
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {nmap_port} --script="(nbstat or smb*) and not (brute or broadcast or dos or external or fuzzer)" --script-args=unsafe=1 -oN "{basedir}/{port}_smb_nmap.txt" -oX "{basedir}/{port}_smb_nmap.xml" {address}
enum4linux -a -M -l -d {address} | tee "{basedir}/{port}_smb_enum4linux.txt"
python2 /usr/share/doc/python-impacket/examples/samrdump.py {address} {port}/SMB | tee "{basedir}/{port}_smb_samrdump.txt"
nbtscan -rvh {address} | tee "{basedir}/{port}_smb_nbtscan.txt"
```



## SNMP (161)
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(snmp*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_snmp_nmap.txt" -oX "{basedir}/{port}_snmp_nmap.xml" {address}
onesixtyone -c data/community -dd -o "{basedir}/{port}_snmp_onesixtyone.txt" {address}
snmpwalk -c public -v 1 {address} | tee "{basedir}/{port}_snmp_snmpwalk.txt"
snmpbulkwalk -c public -v 1 {address} . - kropka na końcu jest ważna
```
```bash
#trzeba zainstalować snmp MIBS żeby widzieć przyjazne nazwy, nie długie  numery
install snmp-mibs-downloader
#i zakomentować linię: mib w pliku 
/etc/snmp/snmp.conf
```
## RDP (3389)
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(rdp*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_rdp_nmap.txt" -oX "{basedir}/{port}_rdp_nmap.xml" {address}
```
## VNC (TCP 5900 – 5906)
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(vnc* or realvnc*) and not (brute or broadcast or dos or external or fuzzer)" --script-args=unsafe=1 -oN "{basedir}/{port}_vnc_nmap.txt" -oX "{basedir}/{port}_vnc_nmap.xml" {address}
```
## Unidentified service
### nmap skrypty
```bash
#TCP
nmap -vv --reason -sV -sC {self.nmapparams} -p {port} --script-args=unsafe=1 -oN "{basedir}/{port}_generic_tcp_nmap.txt" -oX "{basedir}/{port}_generic_tcp_nmap.xml" {address}

#UDP
nmap -vv --reason -sV -sC {self.nmapparams} -sU -p {port} --script-args=unsafe=1 -oN "{basedir}/{port}_generic_udp_nmap.txt" -oX "{basedir}/{port}_generic_udp_nmap.xml" {address}
```
# BAZY DANYCH

## MSSQL
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(ms-sql*) and not (brute or broadcast or dos or external or fuzzer)" --script-args=mssql.instance-port={port},smsql.username-sa,mssql.password-sa -oN "{basedir}/{port}_mssql_nmap.txt" -oX "{basedir}/{port}_mssql_nmap.xml" {address}
```
## MySQL
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(mysql*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_mysql_nmap.txt" -oX "{basedir}/{port}_mysql_nmap.xml" {address}
```

## Oracle
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(oracle*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_oracle_nmap.txt" -oX "{basedir}/{port}_oracle_nmap.xml" {address}
```
## NFS
### nmap skrypty
```bash
nmap -vv --reason -sV {self.nmapparams} -p {port} --script="(rpcinfo or nfs*) and not (brute or broadcast or dos or external or fuzzer)" -oN "{basedir}/{port}_nfs_nmap.txt" -oX "{basedir}/{port}_nfs_nmap.xml" {address}
```
