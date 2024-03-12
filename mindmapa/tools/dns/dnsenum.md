```bash
$ dnsenum <domain> [--dnsserver <DNS_IP/adres>] [-f </usr/share/dnsenum/.>] [-r] # enumerate domain (-r = Recursion on subdomains, brute force all discovered subdomains)
$ dnsenum -p 20 -s 100 --threads 5 <site.com> # Get extra names and subdomains via google scraping
```