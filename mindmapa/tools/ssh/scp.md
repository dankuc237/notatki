opcje jak w ssh (-i ...)
kopiuje poprzez ssh
scp linpeas.sh paul@routerspace:.
scp (co,skąd) (gdzie)  
kopia **pliku** z lokalnej maszyny do zdalne z zachowanem nazwy pliku
```bash
$ scp /home/user_name/filename user_name@IP_zdalne:/home/user_name/
```

kopia **pliku** z lokalnej maszyny do zdalne ze zmianą nazwy nowego pliku
```bash
$ scp /home/user_name/filename user_name@IP_zdalne:/home/user_name/new_filename
```
kopia **folderu** z lokalnej maszyny do zdalne z zachowanem nazwy
```bash
scp /home/user_name/directoryname user_name@IP_zdalne:/home/user_name
```
kopia **folderu** z lokalnej maszyny do zdalne ze zmianą nazwy
```bash
scp /home/user_name/directoryname user_name@IP_zdalne:/home/user_name/new_directoryname
```
