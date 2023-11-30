- [BASH](#bash)
	- [LOGIKA](#logika)
	- [ZMIENNE](#zmienne)
	- [PĘTLE, FUNKCJIE, ITD.](#pętle-funkcjie-itd)
	- [scp](#scp)
	- [find](#find)
	- [unique](#unique)
	- [base64](#base64)
	- [tr](#tr)
	- [sed](#sed)
	- [file](#file)
	- [open\_ssl](#open_ssl)
	- [mkdir](#mkdir)
	- [diff](#diff)
	- [comm](#comm)
	- [crontab](#crontab)
	- [sha256](#sha256)
	- [grep](#grep)
	- [ps](#ps)
	- [kill PID](#kill-pid)
	- [bg/fg / jobs](#bgfg--jobs)
	- [chown/chgrp/chmod/chattr](#chownchgrpchmodchattr)
	- [strings](#strings)
	- [which](#which)
	- [whereis](#whereis)
	- [curl](#curl)
	- [sudo](#sudo)
	- [exiftool](#exiftool)
	- [exec](#exec)
	- [ln](#ln)
	- [unshadow](#unshadow)
	- [Sterowanie dźwiękiem z CLI](#sterowanie-dźwiękiem-z-cli)

# BASH
## LOGIKA
```bash
"A ; B" Run A and then B, regardless of success of A
"A && B" Run B if A succeeded
"A || B" Run B if A failed
"A &" Run A in background.
```
## ZMIENNE
name=variable (bez spacji)  
\$variable zastępuje zmienną jej wartością  
user=\$(whoami) -command substitution  
\$0 -nazwa skruptu  
\$1-9 -9 argunemtów przekazanych do skryptu  
\$@ -wszystkie argumenty przekazane do skryptu  
$? -exit status ostatniego skryptu (0 true, 1 false)  
```bash
if [ $? -eq 0 ]; then
#do something
else
#do something else
fi
```

\$$ -proces ID skryptu  
\$USER -username uruchamiającego skrypt  
$HOSTNAME -hostname maszyny uruchamiającej skrypt  

read answear -przypisane odpowiedzi usera (w CLI) do zmiennej answear  
-p -prompt, wyświetl napis zachęty  
-s -silent, nie widać co jest wpisywane  
```bash
read -p "Username: "
read -ps "Password: "
```

---
## PĘTLE, FUNKCJIE, ITD.
**IF**
```bash
if [test]
	then
		action1
elif [test2]
	then
		action2
else
		action3
fi
```
**WHILE**
```bash
while [test]
do
	action
done
```
**FOR**
```bash
for var_name in list
do
	action
done
```
**listy**
((c=1; c<=10;c++)) ==  {1..10} == 1,2,3,4,5,6,7,8,9,10  
z krokiem => {1..10..2} == 1,3,5,7,9
```bash
echo {1..10..2}
for ((c=1;c<=10;c++));do echo $c; done
```

---


## scp
opcje jak w ssh (-i ...)
kopiuje poprzez ssh
scp linpeas.sh paul@routerspace:.
scp (co,skąd) (gdzie)  
kopia **pliku** z lokalnej maszyny do zdalne z zachowanem nazwy pliku
```bash
scp /home/user_name/filename user_name@IP_zdalne:/home/user_name/
```
kopia **pliku** z lokalnej maszyny do zdalne ze zmianą nazwy nowego pliku
```bash
scp /home/user_name/filename user_name@IP_zdalne:/home/user_name/new_filename
```
kopia **folderu** z lokalnej maszyny do zdalne z zachowanem nazwy
```bash
scp /home/user_name/directoryname user_name@IP_zdalne:/home/user_name
```
kopia **folderu** z lokalnej maszyny do zdalne ze zmianą nazwy
```bash
scp /home/user_name/directoryname user_name@IP_zdalne:/home/user_name/new_directoryname
```

## find
```bash
find /(gdzie) -type f ...(jakie właściwości)
```
|                                                                    |                                                                                                                                     |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `-not`                                                             | neguje następny filtr                                                                                                               |
| `-name`/`-iname`                                                   | nazwa/case insensitive                                                                                                              |
| `-regex`                                                           | filename pasuje do regex (cała scieżka bezwzględna się liczy)                                                                       |
| `-user`                                                            | właściciel                                                                                                                          |
| `-group`                                                           | grupa                                                                                                                               |
| `-perm`                                                            | permisions                                                                                                                          |
| `-executable`                                                      | pliki wykonywalne i foldery, które można przeszukać                                                                                 |
| `-type`<br> `b`<br>`c`<br>`d`<br>`f`<br>`l`<br>`p`<br>`s`          | typ<br>block special file<br>character special file<br>directory<br>normal file<br>symbolic link<br>named pipe<br>socket<br>        |
| `-size`:<br>`+n`<br>`-n`<br>`n`<br>`c`<br>`w`<br>`k`<br>`M`<br>`G` | rozmiar pliku<br>for greater than n,<br>for less than n,<br>for exactly n.<br>bajt (1 char)<br>2 byte words<br>kilo<br>mega<br>giga |
## unique
* -c -zlicza ilość wartości
trzeba wcześniej sortować, inaczej nie zadziała
## base64
base64 encode/decode data and print to standard output
-d -decode
## tr
translate/delete chars
```bash
echo daniel | tr 'a-z' 'A-Z'
```
zmieni wszystko w plku daniel na duze litery
## sed
Stream EDitor
```bash
sed -i 's/word1/word2/g' input.txt
## you can change the delimiter to keep syntax simple or use "/" in searched word
sed -i 's+word1+word2+g' input.txt
sed -i 's_word1_word2_g' input.txt
# w onelinerze
... | sed 's_word1_word2_g'
```
find all occurrences of ‘old-text’ and replace with ‘new-text’ in a file named input.txt (plik zostaje zamieniony w miejscu)

|        |                                                                                                                                             |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `-i`   | in place                                                                                                                                    |
| `-E`   | use extended regular expressions                                                                                                            |
| `s...` | is the substitute command of sed for find and replace                                                                                       |
| `...g` | global replace i.e. find all occurrences of foo and replace with bar using sed. If you removed the `...g` only first occurrence is changed. |

Replace strings in files with bash string manipulation operators only
```bash
${variable/pattern/string}
${variable/find/replace}
#Find and replace all occurrences #
${variable//pattern/string}
```

## file
info na temat pliku
## open_ssl
connect IP:Port
## mkdir
* -p make parent directory jeśli podana jest nie istniejąca ścierzka do tworzonego folderu
## diff
pokaż różnice  w plikach
diff file1 file2
## comm
porównaj pliki
```bash
comm file1 file2 
```
* -1/2/3/12/13/23 -nie wyświetlaj odpowiednich kolumn (1-plik1, 2-plik2, 3-część wspólna)
## crontab
@reboot -wykonaj polecenie po każdym reboocie
* -e -edit user job
* -l -list user jobs
* -r -delete all user jobs
* -i -prompt before del job
## sha256
sha256 file1
checksum of file
## grep 
```bash
grep expresion file
```
extract lines from file
* --invert-match / -i -odwrócone szukanie-wskazuje to co **nie** zawiera

## ps 
list shell proceses
* -e -every process
## kill PID
kill process
## bg/fg / jobs
send process to background/foreground / show shell bg jobs 
## chown/chgrp/chmod/chattr
owner/group/rights/attributes of file

## strings
print the sequences of printable characters in files
## which
finds the binary executable of the program (if it is in your PATH).
## whereis
whereis command also searches for programs that are not present in the PATH setting
## curl
pobiera zawartość z linku
```bash
curl --silent http://late
```
* --silent -nie wyświetlaj paska postępu
* -o *nazwa_pliku* -zapisz plik pod nazwą *nazwa_pliku*
## sudo 
* -l -list user's privileges or check a specific command; use twice for longer format

## exiftool
pozwala na manipulację obrazami, zmianę metadanych itd. 
```bash
exiftool -Artist="tekst"  clean0.png
```
tagi: https://exiftool.org/TagNames/
magic numbers / file signatures: https://en.wikipedia.org/wiki/List_of_file_signatures

## exec
is used to spawn a process that will overtake current process's PID
## ln
create link
```bash
ln f1 f2
```
utwórz link do f1 o nazwie f2
```bash
ln -s f1 f2 
```
-s -symbolic link
## unshadow
```bash
unshadow <passwd> <shadow> > <output.txt>
```
command to combines the < passwd> and <output.txt> files to one file.
shadow zawiera hashe haseł

## Sterowanie dźwiękiem z CLI
```bash
pactl list sinks # lista wyjściowych urządzeń dźwiękowych
amixer -c0 # lista wszystkich kontrolerów na karcie dźwiekowej 0
  amixer -c0 | grep "Simple mixer control" # lista nazw wszystkich kontrolerów na karcie 0

# Mute/unmute dźwięku
amixer set <nazwa_kontrolera> mute/unmute  
  amixer set Master mute/unmute # mute/unmute kanał Master (cały dzwięk z komputera)
  amixer -c0 set Speaker/Headphone mute # mute wybranego urządzenia
  # jeśli mute kanału z którego się właśnie korzysta (głośniki) to Master też jest mute i żeby włączyć dzwięk po przełączeniu na słuchwaki trzeba go unmute
  amixer sset Master toggle # przełącz stan kanału master na odwrotnny (mute>unmute, unmute>mute)

# wybór portu (urządzenia) wyjściowego
  pactl set-sink-port alsa_output.pci-0000_00_1f.3.analog-stereo analog-output-speaker	# ustaw urządzenie wyjściowe jako głośniki
  pactl set-sink-port alsa_output.pci-0000_00_1f.3.analog-stereo analog-output-headphones	# ustaw urządzenie wyjśćiowe jako słuchawki

# regulacja głośności
  amixer -c 0 set Master 100% # ustaw masterchannel na 100%
  amixer -c 0 set Headphone 50% # ustaw kanał słuchawek na 50% głośności

# INNE
  sleep 3600; amixer set Master mute		wycisz kanał master po godzinie
```



