
# amass
https://github.com/OWASP/Amass/blob/master/doc/user_guide.md

## enum
for subdomain enumeration. Perform DNS enumeration and network mapping of systems exposed to the Internet
przeszukuje opensource bazy danych w poszukwaniu domen, czy domeny są osiągalne, pokazuje tylko adresy które są osiągalne,  
Typical parameters for DNS enumeration:
```bash
amass enum -v -src -ip -brute -min-for-recursive 2 -d example.com
```
```bash
amass enum -d *domain* -src -ip -dir directory_to_save
```
` -src` -pokaż skąd są dane
* -ip -chcę widzieć adresy ip znalezionego każdego celu
* -brute -bruteforce nazwy subdomen, DNS bruteforce wordlist : */usr/share/amass/wordlists*
* -dir -dir do którego zapisujemy wyniki
 
## intel
Collect open source intelligence for investigation of the target organization
```bash
amas intel -asn numer_ASN_z_enum
```
 `-asn` -An Autonomous System (AS) is a group of one or more IP prefixes (lists of IP addresses accessible on a network) run by one or more network operators that maintain a single, clearly-defined routing policy. Network operators need Autonomous System Numbers (ASNs) to control routing within their networks and to exchange routing information with other Internet Service Providers (ISPs).
### reverse whois lookup
amass intel -whois -d globomantics.com -dir 
## viz
Generate visualizations of enumerations for exploratory analysis
## track
Compare results of enumerations against common target organizations
## db
Manage the graph databases storing the enumeration results
#

# 2. Początkowe skanowanie
```bash
nmap -p 21,22,80,443 10.10.56.0/24
nmap 192.168.18.10-25
nmap 192.168.*.10
nmap localhost
nmap -iL targets.txt
```
znajdź wszystkie hosty z podanego zakresu mające otwarte porty p, wypróbuje każdy adres z puli, * zastąpi liczbami 0-255
```
* -iL -read target specifications from file
* -F - top 100 ports
* -T -speed of scan (0-5)
```
**1.  host discovery** w sieci
```bash
nmap -sn IP
nmap -sn 192.168.0.1-254 **lub** nmap -sn 192.168.0.0/24
```
**2.  port scan** 
```bash
nmap -p- --min-rate=1000 IP
nmap -sU -p- --min-rate=1000 IP
```
 `-sS` domyślnie skan  -niepełny 3 way handshake, stealth("nie zauważalny tak po chuju bo pakiety są puste i podejrzane, zwykły skan mniej się rzuca w oczy")
 `-sT` -skanowanie z pełnym 3 way handshake
 `-sU` skan UDP
 `-p-` -wszystkie porty
 `--open`: Only show open (or possibly open) ports
`--min-rate=1000` 1000 pakietów na s
`--top-ports 20` -20 najczęstrzych portów

**2. Dalsze skanowanie portów**
```
nmap -p {wcześniej znalezione porty} IP -vv -sC -sV
* -vv verbose- więcej "v", więcej opisu
* -sC - --script=default
* -sV -service version
* -O -OS detection
* -oN/-oX/-oS/-oG/-oA <file> -wynik skanowania zapisany w foramtach normal, XML, s|rIpt kIddi3, grepable format, w 3 pierwszych foramtach na raz i nazwa pliku
* --script=  **(folder ze skryptami /usr/share/nmap/scripts)**
	- vuln
	- smb-enum-shares (enumerate smb shares)
	- smb-vuln-ms-010 - czy serwer jest wrażliwy na podatność Eternal Blue 
	- ftp-anon (FTP anonymous login)
	- http-title
* --open
* -A -agresive
```
# 4. gobuster
ma trzy dostępne tryby: „dns”, „dir” i „vhost”. Służą one odpowiednio do brute force zgadywania subdomen, katalogów i plików oraz wirtualnych hostów. **A website behind cloudflare can mess up a scan like this!**
https://erev0s.com/blog/gobuster-directory-dns-and-virtual-hosts-bruteforcing/
https://github.com/OJ/gobuster
## globalne flagi
<details>
<summary>PARAMETERS</summary>

`-t`, `--threads` int -Number of concurrent threads (default 10)

`-w`, `--wordlist string` -Path to the wordlist

`--no-error` Don't display errors

`-z`, `--no-progress` -Don't display progress

`-v` `-verbose`  

`-q`, `--quiet` -Don't print the banner and other noise (errors)

</details>

## 1. DIR mode
```bash
gobuster dir -u <url> -w <wordlist_file.txt> -x <file_extensions>
# -u -target url, np artcorp.htb
# -w -wordlist: /usr/share/dirbuster/... oraz /usr/share/seclist/...
# -x -include file type, search specific file extensions, np.: php,pdf,html,txt,bak
# -e expand mode, viev full urls
# -r follow redirections
```
```
# find images
gobuster dir -u mytarget.com -w path/to/my/awesome/wordlist.txt -e -t 100 -x jpg,jpeg,png,gif,ico
# web interesting files
gobuster dir -u mytarget.com -w path/to/my/awesome/wordlist.txt -e -t 100 -x php,txt,html,htm
```
## 2. VHOST
In vhosts mode the tool is checking if the subdomain exists by visiting the formed url and verifying the IP address.
```
gobuster vhost -w <wordlist.txt> -u <url> -o <output_file.txt>
```
wirtualne hosty na aserwerze http (na jednym hostingu, serwerze można wyświetlać kilka stron)
## 3. DNS
enumerate subdomains on domain
tool attempts to DNS resolve the subdomains and based on that we are given the result.
```
gobuster dns -r 1.1.1.1 -d pluralsight.com -w <wordlist_subdomains> 
# -r resolver
# -d domain name
# -w wordlist of subdomains
```

---
jakieś skrypty, nie wiem o co chodzi ale nie kasuję
 ```
 for el in *;do echo $el;gobuster dns -d artcorp.htb -t 1000 -w $el -q ; done
```
```
#!/bin/bash
lista=$(find . -type f )
for el in $lista
do
        echo "DNS - file: $el"
        gobuster dns -d artcorp.htb -t 1000 -w $el -q >> daniel.txt
done

```
```
gobuster dir -u http://artcorp.htb -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -t 50 -x .txt,.html,.php --no-error
```
 


