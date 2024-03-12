- [amass](#amass)
	- [enum](#enum)
	- [intel](#intel)
		- [reverse whois lookup](#reverse-whois-lookup)
	- [viz](#viz)
	- [track](#track)
	- [db](#db)
- [gobuster](#gobuster)
	- [globalne flagi](#globalne-flagi)
	- [1. DIR mode](#1-dir-mode)
	- [2. VHOST](#2-vhost)
	- [3. DNS](#3-dns)

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

- -ip -chcę widzieć adresy ip znalezionego każdego celu
- -brute -bruteforce nazwy subdomen, DNS bruteforce wordlist : _/usr/share/amass/wordlists_
- -dir -dir do którego zapisujemy wyniki

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


# gobuster

ma trzy dostępne tryby: „dns”, „dir” i „vhost”. Służą one odpowiednio do brute force zgadywania subdomen, katalogów i plików oraz wirtualnych hostów. **A website behind cloudflare can mess up a scan like this!**  
https://erev0s.com/blog/gobuster-directory-dns-and-virtual-hosts-bruteforcing/  
https://github.com/OJ/gobuster

## globalne flagi

|                           |                                                 |
| ------------------------- | ----------------------------------------------- |
| `-t`, `--threads`         | int -Number of concurrent threads (default 10)  |
| `-w`, `--wordlist string` | Path to the wordlist                            |
| `--no-error`              | Don't display errors                            |
| `-z`, `--no-progress`     | Don't display progress                          |
| `-v` `-verbose`           |
| `-q`, `--quiet`           | Don't print the banner and other noise (errors) |


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
