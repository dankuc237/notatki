### Local/Remote
https://www.ssh.com/academy/ssh/tunneling-example  

dobrze wytłumaczone różnice między forwardingiem ssh:  
https://phoenixnap.com/kb/ssh-port-forwarding#ftoc-heading-4  

[What is the difference between Local/Remote/Dynamic SSH tunneling?](https://serverfault.com/questions/272754/what-is-the-difference-between-local-remote-dynamic-ssh-tunneling)

https://www.youtube.com/watch?v=AtuAdk4MwWw

|  | ENTERANCE |  | EXIT |  |
| :--- | :--: | :--: | :--: | ---: |
| **Local** | on your local machine | you have access | to remote resources at |  |
| `ssh -L` | `<[Local_IP:]Local_Port>` | `:` | `<Remote_IP:Remote_Port>` | `user@server` |
| **Remote** | from the remote server address (IP:port) | you have access | to local resources |  |
| `ssh -R` | `<[Remote_IP:]Remote_Port>` | `:` | `<Local_IP:Local_Port>` | `user@server` |
```bash
$ ssh –L 3000:homepc:23 root@mybox
```
![[local_port_forwarding.png]]


### Dynamic
tzw socks proxy
```bash
ssh –D local_port ssh_server_hostname
ssh –D 5534 pnap@ssh.server.com
```
You are now able to configure a local resource, like a browser, to use proxy localhost on port 5534. All traffic originating from that resource is directed through the SSH connections established for the defined port.
ustawienie przeglądarki żeby korzystała z proxy localhost:5534 sprawia, że wysyła wszystko do tunelu.

For dynamic forwarding to work, you would need to configure and enable each application for the SOCKS proxy server.