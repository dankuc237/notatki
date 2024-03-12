http://ffuf.me/
# Use with BURP
```bash
$ ffuf -w <wordlist> -request <request_file> -request-proto http # fuzz with request file, FUZZ word inside od request Protocol to use along with raw request (default: https)
```
**Burp as proxy (dir mode):**
1. Go to proxy settings
2. Add a new proxy listeners
3. Request handling tab > add Redirect to host and port
4. Make `ffuf` request to new proxy point `$ gobuster dir -u http://url.com `
```bash
-replay-proxy <proxy_addres>
-rate (speed /s)
```

# Example usage

```bash
$ ffuf -u <url+"/FUZZ"> -w <wordlist> [-c ][-e .php,.html,.txt] # dir/file discovery, color output, with extensions

$ ffuf -u <url> -w <wordlist> -H "Host: FUZZ.<domain>" -fs 178 # (vhost) subdomain discovery
```

```bash
# response length of false poistive 
$ curl -s -H "Host: kali.only4you.htb" http://only4you.htb | wc -c
178
```

```bash
$ ffuf -w <wordlist> -u <url>/FUZZ -mc all -fs 42 -c -v # **Fuzz file paths from wordlist.txt, match all responses but filter out those with content-size 42. Colored, verbose output.**

$ ffuf -w <wordlist> -u <url> -H "Host: FUZZ" -mc 200 # Fuzz Host-header, match HTTP 200 responses.

$ ffuf -w <wordlist> -u <url> -X POST -H "Content-Type: application/json" \d '{"name": "FUZZ", "anotherkey": "anothervalue"}' -fr "error" # Fuzz POST JSON data. Match all responses not containing text "error".

$ ffuf -w <wordlist1>:PARAM -w <wordlist2>:VAL -u https://example.org/?PARAM=VAL -mr "VAL" -c # Fuzz multiple locations. Match only responses reflecting the value of "VAL" keyword. Colored. [-mode clusterbomb/pitchfork]
```
The order of the wordlists control in what order the requests are sent. In clusterbomb mode (default) ffuf will iterate over the entire first wordlist before moving on to the second item in the second wordlist.

# Porównanie

https://www.youtube.com/watch?v=N1VurPV0s0o

https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html

`https://github.com/ffuf/ffuf/wiki#clusterbomb-mode`

narzędzie do fuzzowania,np.

# ffuf składnia

```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/burp-parameter-names.txt -u http://localhost:8085/update?FUZZ=1 -fs 0
```

## STANDARD FLAGS

| STANDARD FLAGS                        |                                                                                                                    |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `-c`                                  | colorize output                                                                                                    |
| `-w <wordlist>`                       | Wordlist file path and (optional) keyword separated by colon. eg. '/path/to/wordlist:KEYWORD'                      |
| `-u <url>`                            | url                                                                                                                |
| `-t 100`                              | concurent threads                                                                                                  |
| `-e .html,.php,.txt,.pdf`             | Comma separated list of extensions. Extends FUZZ keyword.                                                          |
| `-H "Header: Value"`                  | dodanie nagłówka                                                                                                   |
| `-X`                                  | HTTP method to use (default: GET)                                                                                  |
| `-x http://127.0.0.1:4444`            | Proxy URL (SOCKS5 or HTTP). For example: http://127.0.0.1:8080 or socks5://127.0.0.1:8080                          |
| `-replay-proxy http://127.0.0.1:4444` | prześlij **znalezione**(czyli poprawne) wyniki do proxy (BURP)<br>, wyśle dwa requesty do celu (ffuf i przez burp) |


## REQUEST FILE

| REQUEST FILE                |                                                                   |
| --------------------------- | ----------------------------------------------------------------- |
| `-request <file>`           | File containing the raw http request                              |
| `-request-proto https/http` | Protocol to use along with raw request **(default: https)!!!!!!** |

## MATCH/FILTER request

| MATCH/FILTER |                                                                                              |
| ------------ | -------------------------------------------------------------------------------------------- |
| `-mr`        | **Match regexp**                                                                             |
| `-mc`        | Match HTTP status codes, or **"all" for everything**. (default: 200,204,301,302,307,401,403) |
| `-ml`        | Match amount of lines in response                                                            |
| `-ms`        | Match HTTP response size                                                                     |
| `-mw`        | Match amount of words in response                                                            |
| `-fr`        | Filter regexp                                                                                |
| `-fc`        | Filter HTTP status codes from response. Comma separated list of codes and ranges             |
| `-fl`        | Filter by amount of lines in response. Comma separated list of line counts and ranges        |
| `-fs`        | Filter HTTP response size. Comma separated list of sizes and ranges                          |
| `-fw`        | Filter by amount of words in response. Comma separated list of word counts and ranges        |

## OUTPUT FILE (raport ze znalezisk)

| OUTPUT FILE (raport ze znalezisk) |                                                   |
| --------------------------------- | ------------------------------------------------- |
| `-o out_name`                     | zapisz wynik do pliku (domyślnie w formacie JSON) |
| `-o ./output.md -of md`           | zapisz do pliku output.md, format markdown        |

## REKURSJA

| REKURSJA w fuzzowaniu                         |                                                                                     |
| --------------------------------------------- | ----------------------------------------------------------------------------------- |
| `-recursion`                                  | recursion only works for paths with the HTTP status code of 30X                     |
| `-recursion` <br>`-recursion-strategy greedy` | adds all the matches as recursion jobs, especially meant for API endpoint discovery |

